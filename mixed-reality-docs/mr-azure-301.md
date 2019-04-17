---
title: MR et Azure 301 - traduction linguistique
description: Terminer ce cours pour apprendre à implémenter l’API Azure Translator Text dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, de texte translator text, hololens, immersives, vr
ms.openlocfilehash: 6fe31d1bcb72337f0a3e8664893ea0f7c0540aae
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59596316"
---
>[!NOTE]
><span data-ttu-id="baf2c-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="baf2c-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="baf2c-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="baf2c-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="baf2c-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="baf2c-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="baf2c-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="baf2c-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="baf2c-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="baf2c-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="baf2c-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="baf2c-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-301-language-translation"></a><span data-ttu-id="baf2c-110">MR et Azure 301 : Traduction linguistique</span><span class="sxs-lookup"><span data-stu-id="baf2c-110">MR and Azure 301: Language translation</span></span>

<span data-ttu-id="baf2c-111">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de traduction à une application de réalité mixte à l’aide d’Azure Cognitive Services, avec l’API Translator Text.</span><span class="sxs-lookup"><span data-stu-id="baf2c-111">In this course, you will learn how to add translation capabilities to a mixed reality application using Azure Cognitive Services, with the Translator Text API.</span></span>

![Produit final](images/AzureLabs-Lab1-00.png)

<span data-ttu-id="baf2c-113">L’API Translator Text est une Service qui fonctionne dans quasiment en temps réel de la traduction.</span><span class="sxs-lookup"><span data-stu-id="baf2c-113">The Translator Text API is a translation Service which works in near real-time.</span></span> <span data-ttu-id="baf2c-114">Le Service est basé sur le cloud, et, à l’aide d’un appel d’API REST, une application peut effectuer permet de traduire du texte dans un autre langage de la technologie de traduction automatique NEURONALE.</span><span class="sxs-lookup"><span data-stu-id="baf2c-114">The Service is cloud-based, and, using a REST API call, an app can make use of the neural machine translation technology to translate text to another language.</span></span> <span data-ttu-id="baf2c-115">Pour plus d’informations, visitez le [page de l’API Translator Text Azure](https://azure.microsoft.com/services/cognitive-services/translator-text-api/).</span><span class="sxs-lookup"><span data-stu-id="baf2c-115">For more information, visit the [Azure Translator Text API page](https://azure.microsoft.com/services/cognitive-services/translator-text-api/).</span></span>

<span data-ttu-id="baf2c-116">À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="baf2c-116">Upon completion of this course, you will have a mixed reality application which will be able to do the following:</span></span>

1.  <span data-ttu-id="baf2c-117">L’utilisateur qui s’exprime en un microphone connecté à un casque (VR) immersif (ou le microphone intégré de HoloLens).</span><span class="sxs-lookup"><span data-stu-id="baf2c-117">The user will speak into a microphone connected to an immersive (VR) headset (or the built-in microphone of HoloLens).</span></span>
2.  <span data-ttu-id="baf2c-118">L’application capture la dictée et l’envoyer à l’API Azure Translator Text.</span><span class="sxs-lookup"><span data-stu-id="baf2c-118">The app will capture the dictation and send it to the Azure Translator Text API.</span></span>
3.  <span data-ttu-id="baf2c-119">Le résultat de la traduction s’affichera dans un groupe de l’interface utilisateur simple dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-119">The translation result will be displayed in a simple UI group in the Unity Scene.</span></span>

<span data-ttu-id="baf2c-120">Ce cours va vous apprendre à obtenir les résultats à partir du Service de traduction dans une application basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-120">This course will teach you how to get the results from the Translator Service into a Unity-based sample application.</span></span> <span data-ttu-id="baf2c-121">Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.</span><span class="sxs-lookup"><span data-stu-id="baf2c-121">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="baf2c-122">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="baf2c-122">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="baf2c-123">Cours</span><span class="sxs-lookup"><span data-stu-id="baf2c-123">Course</span></span></th><th style="width:150px"> <span data-ttu-id="baf2c-124"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="baf2c-124"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="baf2c-125"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="baf2c-125"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="baf2c-126">MR et Azure 301 : Traduction linguistique</span><span class="sxs-lookup"><span data-stu-id="baf2c-126">MR and Azure 301: Language translation</span></span></td><td style="text-align: center;"> <span data-ttu-id="baf2c-127">✔️</span><span class="sxs-lookup"><span data-stu-id="baf2c-127">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="baf2c-128">✔️</span><span class="sxs-lookup"><span data-stu-id="baf2c-128">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="baf2c-129">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="baf2c-129">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="baf2c-130">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="baf2c-130">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="baf2c-131">Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.</span><span class="sxs-lookup"><span data-stu-id="baf2c-131">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baf2c-132">Prérequis</span><span class="sxs-lookup"><span data-stu-id="baf2c-132">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="baf2c-133">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="baf2c-133">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="baf2c-134">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="baf2c-134">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="baf2c-135">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="baf2c-135">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="baf2c-136">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="baf2c-136">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="baf2c-137">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="baf2c-137">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="baf2c-138">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="baf2c-138">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="baf2c-139">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="baf2c-139">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="baf2c-140">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="baf2c-140">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="baf2c-141">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="baf2c-141">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="baf2c-142">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="baf2c-142">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="baf2c-143">Un ensemble de casque avec un microphone intégré (si le casque n’a pas un mic intégré et les haut-parleurs)</span><span class="sxs-lookup"><span data-stu-id="baf2c-143">A set of headphones with a built-in microphone (if the headset doesn't have a built-in mic and speakers)</span></span>
- <span data-ttu-id="baf2c-144">Accès à Internet pour la récupération Azure le programme d’installation et de traduction</span><span class="sxs-lookup"><span data-stu-id="baf2c-144">Internet access for Azure setup and translation retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="baf2c-145">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="baf2c-145">Before you start</span></span>

- <span data-ttu-id="baf2c-146">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="baf2c-146">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
- <span data-ttu-id="baf2c-147">Le code dans ce didacticiel vous permettra d’enregistrer à partir de l’appareil de microphone par défaut connecté à votre PC.</span><span class="sxs-lookup"><span data-stu-id="baf2c-147">The code in this tutorial will allow you to record from the default microphone device connected to your PC.</span></span> <span data-ttu-id="baf2c-148">Assurez-vous que l’appareil de microphone par défaut est définie sur l’appareil que vous prévoyez d’utiliser pour capturer votre voix.</span><span class="sxs-lookup"><span data-stu-id="baf2c-148">Make sure the default microphone device is set to the device you plan to use to capture your voice.</span></span>
- <span data-ttu-id="baf2c-149">Pour permettre à votre PC activer la dictée, accédez à **Paramètres > confidentialité > vocale, la saisie manuscrite & tapant** et sélectionnez le bouton **sur Activer le services de reconnaissance vocale et les suggestions en tapant**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-149">To allow your PC to enable dictation, go to **Settings > Privacy > Speech, inking & typing** and select the button **Turn On speech services and typing suggestions**.</span></span>
- <span data-ttu-id="baf2c-150">Si vous utilisez un microphone et le casque (ou intégré à) votre casque, assurez-vous que l’option « Lorsque je wear mon casque, basculez vers casque mic » est activée dans **Paramètres > une réalité mixte > Audio et reconnaissance vocale**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-150">If you're using a microphone and headphones connected to (or built-in to) your headset, make sure the option “When I wear my headset, switch to headset mic” is turned on in **Settings > Mixed reality > Audio and speech**.</span></span>

   ![Paramètres de la réalité mixte](images/AzureLabs-Lab1-00-5.png)

   ![Paramètre du microphone](images/AzureLabs-Lab1-01.png)

> [!WARNING]
> <span data-ttu-id="baf2c-153">N’oubliez pas que si vous développez pour un casque immersif pour ce laboratoire, vous pouvez rencontrer des problèmes de périphérique de sortie audio.</span><span class="sxs-lookup"><span data-stu-id="baf2c-153">Be aware that if you are developing for an immersive headset for this lab, you may experience audio output device issues.</span></span> <span data-ttu-id="baf2c-154">Il s’agit d’un problème avec Unity, ce qui a été résolu dans les versions ultérieures de Unity (Unity 2018.2).</span><span class="sxs-lookup"><span data-stu-id="baf2c-154">This is due to an issue with Unity, which is fixed in later versions of Unity (Unity 2018.2).</span></span> <span data-ttu-id="baf2c-155">Le problème empêche la modification le périphérique de sortie audio par défaut au moment de l’exécution d’Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-155">The issue prevents Unity from changing the default audio output device at run time.</span></span> <span data-ttu-id="baf2c-156">Pour contourner ce problème, assurez-vous de qu'avoir effectué les étapes ci-dessus et fermez et rouvrez l’éditeur, lorsque ce problème se présente.</span><span class="sxs-lookup"><span data-stu-id="baf2c-156">As a work around, ensure you have completed the above steps, and close and re-open the Editor, when this issue presents itself.</span></span>

## <a name="chapter-1--the-azure-portal"></a><span data-ttu-id="baf2c-157">Chapitre 1 – le portail Azure</span><span class="sxs-lookup"><span data-stu-id="baf2c-157">Chapter 1 – The Azure Portal</span></span>

<span data-ttu-id="baf2c-158">Pour utiliser l’API de Translator Azure, vous devrez configurer une instance du Service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="baf2c-158">To use the Azure Translator API, you will need to configure an instance of the Service to be made available to your application.</span></span>

1.  <span data-ttu-id="baf2c-159">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="baf2c-159">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="baf2c-160">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="baf2c-160">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="baf2c-161">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="baf2c-161">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="baf2c-162">Une fois que vous êtes connecté, cliquez sur **New** dans le coin supérieur gauche supérieur et recherchez « API Translator Text. »</span><span class="sxs-lookup"><span data-stu-id="baf2c-162">Once you are logged in, click on **New** in the top left corner and search for "Translator Text API."</span></span> <span data-ttu-id="baf2c-163">Sélectionnez **entrez**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-163">Select **Enter**.</span></span>

    ![Nouvelle ressource](images/AzureLabs-Lab1-02.png)

    > [!NOTE]
    > <span data-ttu-id="baf2c-165">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="baf2c-165">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="baf2c-166">La nouvelle page doit fournir une description de la *API Translator Text* Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-166">The new page will provide a description of the *Translator Text API* Service.</span></span> <span data-ttu-id="baf2c-167">En bas à gauche de cette page, sélectionnez le **créer** bouton, pour créer une association avec ce Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-167">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Créer le Service d’API Translator Text](images/AzureLabs-Lab1-03.png)

4.  <span data-ttu-id="baf2c-169">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="baf2c-169">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="baf2c-170">Insérez votre souhaitée **nom** pour cette instance de Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-170">Insert your desired **Name** for this Service instance.</span></span>
    2. <span data-ttu-id="baf2c-171">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-171">Select an appropriate **Subscription**.</span></span>
    3. <span data-ttu-id="baf2c-172">Sélectionnez le **niveau tarifaire** appropriés pour vous, s’il s’agit du premier temps à créer un *Service de texte Translator*, un niveau gratuit (nommé F0) doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="baf2c-172">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Translator Text Service*, a free tier (named F0) should be available to you.</span></span>
    4. <span data-ttu-id="baf2c-173">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="baf2c-173">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="baf2c-174">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="baf2c-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="baf2c-175">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="baf2c-175">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="baf2c-176">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="baf2c-176">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="baf2c-177">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="baf2c-177">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="baf2c-178">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="baf2c-178">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="baf2c-179">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="baf2c-179">Some Azure assets are only available in certain regions.</span></span>
    6. <span data-ttu-id="baf2c-180">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-180">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="baf2c-181">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-181">Select **Create**.</span></span>

        ![Sélectionnez le bouton Créer.](images/AzureLabs-Lab1-04.png)

5.  <span data-ttu-id="baf2c-183">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="baf2c-183">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="baf2c-184">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="baf2c-184">A notification will appear in the portal once the Service instance is created.</span></span> 

    ![Notification de la création du Service Azure](images/AzureLabs-Lab1-05.png)

7.  <span data-ttu-id="baf2c-186">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-186">Click on the notification to explore your new Service instance.</span></span> 

    ![Accédez au menu contextuel de ressources.](images/AzureLabs-Lab1-06.png)

8.  <span data-ttu-id="baf2c-188">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-188">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="baf2c-189">Vous êtes redirigé vers votre nouvelle instance de Service d’API Translator Text.</span><span class="sxs-lookup"><span data-stu-id="baf2c-189">You will be taken to your new Translator Text API Service instance.</span></span> 

    ![Page du Service d’API de texte Translator](images/AzureLabs-Lab1-07.png)

9.  <span data-ttu-id="baf2c-191">Dans ce didacticiel, votre application devra effectuer des appels à votre Service, par l’intermédiaire à l’aide de la clé d’abonnement de votre Service.</span><span class="sxs-lookup"><span data-stu-id="baf2c-191">Within this tutorial, your application will need to make calls to your Service, which is done through using your Service’s Subscription Key.</span></span> 
10. <span data-ttu-id="baf2c-192">À partir de la *Guide de démarrage rapide* page de votre *Translator Text* Service, accédez à la première étape, *récupérez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur le lien hypertexte bleu clés, situé dans le menu de navigation de Services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="baf2c-192">From the *Quick start* page of your *Translator Text* Service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the Services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="baf2c-193">Cela permet de révéler votre Service *clés*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-193">This will reveal your Service *Keys*.</span></span>
11. <span data-ttu-id="baf2c-194">Effectuez une copie de l’une des clés affichées, car vous en aurez besoin plus loin dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="baf2c-194">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 

## <a name="chapter-2--set-up-the-unity-project"></a><span data-ttu-id="baf2c-195">Chapitre 2 : configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="baf2c-195">Chapter 2 – Set up the Unity project</span></span>

<span data-ttu-id="baf2c-196">Configurer et tester votre casque immersives de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="baf2c-196">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE]
> <span data-ttu-id="baf2c-197">Vous n'aurez pas besoin des contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="baf2c-197">You will not need motion controllers for this course.</span></span> <span data-ttu-id="baf2c-198">Si vous avez besoin de prendre en charge de la configuration d’un casque immersive, veuillez [suivez ces étapes](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="baf2c-198">If you need support setting up an immersive headset, please [follow these steps](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

<span data-ttu-id="baf2c-199">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et, par conséquent, est un bon modèle pour d’autres projets :</span><span class="sxs-lookup"><span data-stu-id="baf2c-199">The following is a typical set up for developing with mixed reality and, as such, is a good template for other projects:</span></span>

1.  <span data-ttu-id="baf2c-200">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-200">Open *Unity* and click **New**.</span></span> 

    ![Démarrer un nouveau projet Unity.](images/AzureLabs-Lab1-08.png)

2.  <span data-ttu-id="baf2c-202">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-202">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="baf2c-203">Insérer **MR_Translation**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-203">Insert **MR_Translation**.</span></span> <span data-ttu-id="baf2c-204">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-204">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="baf2c-205">Définir le *emplacement* à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="baf2c-205">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="baf2c-206">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-206">Then, click **Create project**.</span></span>

    ![Fournissent des détails pour un projet Unity.](images/AzureLabs-Lab1-09.png)

3.  <span data-ttu-id="baf2c-208">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-208">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="baf2c-209">Accédez à **Modifier > Préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-209">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="baf2c-210">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-210">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="baf2c-211">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="baf2c-211">Close the **Preferences** window.</span></span>

    ![Mettre à jour les préférences de l’éditeur de script.](images/AzureLabs-Lab1-10.png)

4.  <span data-ttu-id="baf2c-213">Ensuite, accédez à **fichier > Paramètres de Build** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le **plateforme basculer** bouton.</span><span class="sxs-lookup"><span data-stu-id="baf2c-213">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres, plateforme de commutation à UWP de la génération.](images/AzureLabs-Lab1-11.png)

5.  <span data-ttu-id="baf2c-215">Accédez à **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="baf2c-215">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="baf2c-216">**Équipement cible** a la valeur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-216">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="baf2c-217">Pour Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-217">For Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="baf2c-218">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="baf2c-218">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="baf2c-219">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="baf2c-219">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="baf2c-220">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="baf2c-220">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="baf2c-221">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="baf2c-221">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="baf2c-222">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="baf2c-222">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="baf2c-223">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-223">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="baf2c-224">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="baf2c-224">A save window will appear.</span></span>

            ![Cliquez sur Ajouter un bouton scènes ouvert](images/AzureLabs-Lab1-12.png)

        2. <span data-ttu-id="baf2c-226">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-226">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un nouveau dossier de scripts](images/AzureLabs-Lab1-13.png)

        3. <span data-ttu-id="baf2c-228">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier*: champ de texte, tapez **MR_TranslationScene**, puis appuyez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-228">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_TranslationScene**, then press **Save**.</span></span>

            ![Donnez un nom à nouvelle scène.](images/AzureLabs-Lab1-14.png)

            > <span data-ttu-id="baf2c-230">N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-230">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity Project.</span></span> <span data-ttu-id="baf2c-231">Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-231">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7. <span data-ttu-id="baf2c-232">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="baf2c-232">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="baf2c-233">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="baf2c-233">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab1-15.png)

7. <span data-ttu-id="baf2c-235">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="baf2c-235">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="baf2c-236">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="baf2c-236">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="baf2c-237">**Version du Runtime de script** doit être **Stable** (équivalent .NET 3.5).</span><span class="sxs-lookup"><span data-stu-id="baf2c-237">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="baf2c-238">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="baf2c-238">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="baf2c-239">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="baf2c-239">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettre à jour les autres paramètres.](images/AzureLabs-Lab1-16.png)
      
    2. <span data-ttu-id="baf2c-241">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="baf2c-241">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="baf2c-242">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="baf2c-242">**InternetClient**</span></span>
        2. <span data-ttu-id="baf2c-243">**Microphone**</span><span class="sxs-lookup"><span data-stu-id="baf2c-243">**Microphone**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab1-17.png)

    3. <span data-ttu-id="baf2c-245">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="baf2c-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettre à jour les paramètres de R X.](images/AzureLabs-Lab1-18.png)

8.  <span data-ttu-id="baf2c-247">Dans **paramètres de Build**, *Unity C# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="baf2c-247">Back in **Build Settings**, *Unity C# Projects* is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="baf2c-248">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="baf2c-248">Close the Build Settings window.</span></span>
10. <span data-ttu-id="baf2c-249">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="baf2c-249">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-3--main-camera-setup"></a><span data-ttu-id="baf2c-250">Chapitre 3 – le programme d’installation de la caméra principale</span><span class="sxs-lookup"><span data-stu-id="baf2c-250">Chapter 3 – Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="baf2c-251">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à [télécharger cette .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20301%20-%20Language%20translation/Azure-MR-301.unitypackage), importez-le dans votre projet en tant qu’un [ *Package personnalisé*](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 5](#chapter-5--create-the-results-class).</span><span class="sxs-lookup"><span data-stu-id="baf2c-251">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20301%20-%20Language%20translation/Azure-MR-301.unitypackage), import it into your project as a [*Custom Package*](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-results-class).</span></span> <span data-ttu-id="baf2c-252">Vous devez toujours créer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-252">You will still need to create a Unity Project.</span></span>

1.  <span data-ttu-id="baf2c-253">Dans le *hiérarchie panneau*, vous trouverez un objet appelé **Main Camera**, cet objet représente votre point de vue du « head » une fois que vous êtes « à l’intérieur » de votre application.</span><span class="sxs-lookup"><span data-stu-id="baf2c-253">In the *Hierarchy Panel*, you will find an object called **Main Camera**, this object represents your “head” point of view once you are “inside” your application.</span></span>
2.  <span data-ttu-id="baf2c-254">Avec le tableau de bord Unity devant vous, sélectionnez le **GameObject de caméra principale**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-254">With the Unity Dashboard in front of you, select the **Main Camera GameObject**.</span></span> <span data-ttu-id="baf2c-255">Vous remarquerez que le *panneau Inspecteur* (généralement situé vers la droite, dans le tableau de bord) affiche les différents composants de qui *GameObject*, avec *transformer* en haut, suivie de *caméra*et certains autres composants.</span><span class="sxs-lookup"><span data-stu-id="baf2c-255">You will notice that the *Inspector Panel* (generally found to the right, within the Dashboard) will show the various components of that *GameObject*, with *Transform* at the top, followed by *Camera*, and some other components.</span></span> <span data-ttu-id="baf2c-256">Vous devez réinitialiser la transformation de la caméra principale, donc il est positionné correctement.</span><span class="sxs-lookup"><span data-stu-id="baf2c-256">You will need to reset the Transform of the Main Camera, so it is positioned correctly.</span></span>
3.  <span data-ttu-id="baf2c-257">Pour ce faire, sélectionnez le **ENGRENAGE** icône en regard de la caméra *transformer* composant, puis en sélectionnant **réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-257">To do this, select the **Gear** icon next to the Camera’s *Transform* component, and selecting **Reset**.</span></span> 

    ![Réinitialiser la transformation Main Camera.](images/AzureLabs-Lab1-19.png)
 
4.  <span data-ttu-id="baf2c-259">Le *transformer* composant doit alors ressembler :</span><span class="sxs-lookup"><span data-stu-id="baf2c-259">The *Transform* component should then look like:</span></span>

    1. <span data-ttu-id="baf2c-260">Le *Position* a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="baf2c-260">The *Position* is set to **0, 0, 0**</span></span>
    2. <span data-ttu-id="baf2c-261">*Rotation* a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="baf2c-261">*Rotation* is set to **0, 0, 0**</span></span>
    3. <span data-ttu-id="baf2c-262">Et *mise à l’échelle* a la valeur **1, 1, 1**</span><span class="sxs-lookup"><span data-stu-id="baf2c-262">And *Scale* is set to **1, 1, 1**</span></span>

        ![Transformer les informations pour l’appareil photo](images/AzureLabs-Lab1-20.png)

5.  <span data-ttu-id="baf2c-264">Ensuite, avec le **Main Camera** de l’objet sélectionné, consultez le **ajouter un composant** bouton situé tout en bas de la *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-264">Next, with the **Main Camera** object selected, see the **Add Component** button located at the very bottom of the *Inspector Panel*.</span></span> 
6.  <span data-ttu-id="baf2c-265">Sélectionnez ce bouton, puis rechercher (soit en saisissant *Audio Source* dans le champ de recherche ou de la navigation dans les sections) pour le composant appelé **Audio Source** comme indiqué ci-dessous et sélectionnez-le (appuyez sur entrée sur ce dernier fonctionne également).</span><span class="sxs-lookup"><span data-stu-id="baf2c-265">Select that button, and search (by either typing *Audio Source* into the search field or navigating the sections) for the component called **Audio Source** as shown below and select it (pressing enter on it also works).</span></span>
7.  <span data-ttu-id="baf2c-266">Un *Audio Source* composant sera ajouté à la **Main Camera**, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="baf2c-266">An *Audio Source* component will be added to the **Main Camera**, as demonstrated below.</span></span>

    ![Ajoutez un composant de Source de données Audio.](images/AzureLabs-Lab1-21.png)

    > [!NOTE]
    > <span data-ttu-id="baf2c-268">Pour Microsoft HoloLens, vous devez également modifier les paramètres suivants, qui font partie de la **caméra** composant sur votre **Main Camera**:</span><span class="sxs-lookup"><span data-stu-id="baf2c-268">For Microsoft HoloLens, you will need to also change the following, which are part of the **Camera** component on your **Main Camera**:</span></span>
    > - <span data-ttu-id="baf2c-269">**Effacer les indicateurs :** Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="baf2c-269">**Clear Flags:** Solid Color.</span></span>
    > - <span data-ttu-id="baf2c-270">**Arrière-plan** ' noir, Alpha 0' – couleur hexadécimale : #00000000.</span><span class="sxs-lookup"><span data-stu-id="baf2c-270">**Background** ‘Black, Alpha 0’ – Hex color: #00000000.</span></span>

## <a name="chapter-4--setup-debug-canvas"></a><span data-ttu-id="baf2c-271">Chapitre 4 – le programme d’installation débogage canevas</span><span class="sxs-lookup"><span data-stu-id="baf2c-271">Chapter 4 – Setup Debug Canvas</span></span>

<span data-ttu-id="baf2c-272">Pour afficher l’entrée et la sortie de la traduction, une interface utilisateur de base doit être créé.</span><span class="sxs-lookup"><span data-stu-id="baf2c-272">To show the input and output of the translation, a basic UI needs to be created.</span></span> <span data-ttu-id="baf2c-273">Pour ce cours, vous allez créer un objet de l’interface utilisateur de la zone de dessin, avec plusieurs objets 'Text' pour afficher les données.</span><span class="sxs-lookup"><span data-stu-id="baf2c-273">For this course, you will create a Canvas UI object, with several ‘Text’ objects to show the data.</span></span>

1.  <span data-ttu-id="baf2c-274">Avec le bouton droit dans une zone vide de la *hiérarchie panneau*, sous **l’interface utilisateur**, ajouter un **canevas**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-274">Right-click in an empty area of the *Hierarchy Panel*, under **UI**, add a **Canvas**.</span></span>

    ![Ajouter un nouvel objet de l’interface utilisateur de la zone de dessin.](images/AzureLabs-Lab1-22.png)

2.  <span data-ttu-id="baf2c-276">Avec l’objet de zone de dessin sélectionné, dans le *panneau Inspecteur* (dans le composant « Canevas »), modifiez **Mode de rendu** à **espace universel**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-276">With the Canvas object selected, in the *Inspector Panel* (within the ‘Canvas’ component), change **Render Mode** to **World Space**.</span></span> 
3.  <span data-ttu-id="baf2c-277">Ensuite, modifiez les paramètres suivants dans le *Rect transformation du panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="baf2c-277">Next, change the following parameters in the *Inspector Panel’s Rect Transform*:</span></span>

    1. <span data-ttu-id="baf2c-278">*POS* -  **X** 0 **Y** 0 **Z** 40</span><span class="sxs-lookup"><span data-stu-id="baf2c-278">*POS* -  **X** 0 **Y** 0 **Z** 40</span></span>
    2. <span data-ttu-id="baf2c-279">*Largeur* - 500</span><span class="sxs-lookup"><span data-stu-id="baf2c-279">*Width* -    500</span></span>
    3. <span data-ttu-id="baf2c-280">*Hauteur* - 300</span><span class="sxs-lookup"><span data-stu-id="baf2c-280">*Height* -   300</span></span>
    4. <span data-ttu-id="baf2c-281">*Mise à l’échelle* - **X** 0.13 **Y** 0.13 **Z** 0,13</span><span class="sxs-lookup"><span data-stu-id="baf2c-281">*Scale* - **X** 0.13 **Y** 0.13  **Z** 0.13</span></span>

        ![Mettre à jour de la transformation de rect pour la zone de dessin.](images/AzureLabs-Lab1-23.png)
 
4.  <span data-ttu-id="baf2c-283">Cliquez avec le bouton droit sur le **canevas** dans le *hiérarchie panneau*, sous **l’interface utilisateur**et ajoutez un **panneau**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-283">Right click on the **Canvas** in the *Hierarchy Panel*, under **UI**, and add a **Panel**.</span></span> <span data-ttu-id="baf2c-284">Cela **panneau** fournira un arrière-plan au texte que vous devez afficher dans la scène.</span><span class="sxs-lookup"><span data-stu-id="baf2c-284">This **Panel** will provide a background to the text that you will be displaying in the scene.</span></span>
5.  <span data-ttu-id="baf2c-285">Cliquez avec le bouton droit sur le **panneau** dans le *hiérarchie panneau*, sous **l’interface utilisateur**et ajoutez un **textuel**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-285">Right click on the **Panel** in the *Hierarchy Panel*, under **UI**, and add a **Text object**.</span></span> <span data-ttu-id="baf2c-286">Répétez ce processus jusqu'à ce que vous avez créé quatre objets de textes d’interface utilisateur au total (Conseil : Si vous avez le premier objet de 'Text' sélectionné, vous pouvez simplement appuyer sur **« Ctrl » + avait '**, dupliquer, jusqu'à ce que vous ayez quatre au total).</span><span class="sxs-lookup"><span data-stu-id="baf2c-286">Repeat the same process until you have created four UI Text objects in total (Hint: if you have the first ‘Text’ object selected, you can simply press **‘Ctrl’ + ‘D’**, to duplicate it, until you have four in total).</span></span> 
6.  <span data-ttu-id="baf2c-287">Pour chaque **textuel**, sélectionnez-le, puis utilisez le ci-dessous tables pour définir les paramètres le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-287">For each **Text Object**, select it and use the below tables to set the parameters in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="baf2c-288">Pour le *Rect transformation* composant :</span><span class="sxs-lookup"><span data-stu-id="baf2c-288">For the *Rect Transform* component:</span></span>

        | <span data-ttu-id="baf2c-289">Nom</span><span class="sxs-lookup"><span data-stu-id="baf2c-289">Name</span></span>                   | <span data-ttu-id="baf2c-290">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="baf2c-290">Transform - *Position*</span></span>             | <span data-ttu-id="baf2c-291">Largeur</span><span class="sxs-lookup"><span data-stu-id="baf2c-291">Width</span></span>      | <span data-ttu-id="baf2c-292">Hauteur</span><span class="sxs-lookup"><span data-stu-id="baf2c-292">Height</span></span>    |
        |:----------------------:|:----------------------------------:|:----------:|:---------:|
        | <span data-ttu-id="baf2c-293">MicrophoneStatusLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-293">MicrophoneStatusLabel</span></span>  | <span data-ttu-id="baf2c-294">**X** -80 **Y** 90 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-294">**X** -80 **Y** 90 **Z** 0</span></span>         | <span data-ttu-id="baf2c-295">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-295">300</span></span>        | <span data-ttu-id="baf2c-296">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-296">30</span></span>        |
        | <span data-ttu-id="baf2c-297">AzureResponseLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-297">AzureResponseLabel</span></span>     | <span data-ttu-id="baf2c-298">**X** -80 **Y** 30 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-298">**X** -80 **Y** 30 **Z** 0</span></span>         | <span data-ttu-id="baf2c-299">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-299">300</span></span>        | <span data-ttu-id="baf2c-300">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-300">30</span></span>        |
        | <span data-ttu-id="baf2c-301">DictationLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-301">DictationLabel</span></span>         | <span data-ttu-id="baf2c-302">**X** -80 **Y** -30 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-302">**X** -80 **Y** -30 **Z** 0</span></span>        | <span data-ttu-id="baf2c-303">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-303">300</span></span>        | <span data-ttu-id="baf2c-304">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-304">30</span></span>        |
        | <span data-ttu-id="baf2c-305">TranslationResultLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-305">TranslationResultLabel</span></span> | <span data-ttu-id="baf2c-306">**X** -80 **Y** -90 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-306">**X** -80 **Y** -90 **Z** 0</span></span>        | <span data-ttu-id="baf2c-307">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-307">300</span></span>        | <span data-ttu-id="baf2c-308">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-308">30</span></span>        |


    2. <span data-ttu-id="baf2c-309">Pour le **texte (Script)** composant :</span><span class="sxs-lookup"><span data-stu-id="baf2c-309">For the **Text (Script)** component:</span></span>


        | <span data-ttu-id="baf2c-310">Nom</span><span class="sxs-lookup"><span data-stu-id="baf2c-310">Name</span></span>                   | <span data-ttu-id="baf2c-311">Text</span><span class="sxs-lookup"><span data-stu-id="baf2c-311">Text</span></span>               | <span data-ttu-id="baf2c-312">Taille de police</span><span class="sxs-lookup"><span data-stu-id="baf2c-312">Font Size</span></span>    |
        |:----------------------:|:------------------:|:------------:|
        | <span data-ttu-id="baf2c-313">MicrophoneStatusLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-313">MicrophoneStatusLabel</span></span>  | <span data-ttu-id="baf2c-314">État du microphone :</span><span class="sxs-lookup"><span data-stu-id="baf2c-314">Microphone Status:</span></span> | <span data-ttu-id="baf2c-315">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-315">20</span></span>           |
        | <span data-ttu-id="baf2c-316">AzureResponseLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-316">AzureResponseLabel</span></span>     | <span data-ttu-id="baf2c-317">Réponse Web Azure</span><span class="sxs-lookup"><span data-stu-id="baf2c-317">Azure Web Response</span></span> | <span data-ttu-id="baf2c-318">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-318">20</span></span>           |
        | <span data-ttu-id="baf2c-319">DictationLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-319">DictationLabel</span></span>         |   <span data-ttu-id="baf2c-320">Vous l’avez dit simplement :</span><span class="sxs-lookup"><span data-stu-id="baf2c-320">You just said:</span></span>   | <span data-ttu-id="baf2c-321">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-321">20</span></span>           |
        | <span data-ttu-id="baf2c-322">TranslationResultLabel</span><span class="sxs-lookup"><span data-stu-id="baf2c-322">TranslationResultLabel</span></span> |    <span data-ttu-id="baf2c-323">Traduction :</span><span class="sxs-lookup"><span data-stu-id="baf2c-323">Translation:</span></span>    | <span data-ttu-id="baf2c-324">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-324">20</span></span>           |

        ![Entrez les valeurs correspondantes pour les étiquettes de l’interface utilisateur.](images/AzureLabs-Lab1-24.png)

    3. <span data-ttu-id="baf2c-326">En outre, que le Style de police **gras**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-326">Also, make the Font Style **Bold**.</span></span> <span data-ttu-id="baf2c-327">Cela facilite le texte à lire.</span><span class="sxs-lookup"><span data-stu-id="baf2c-327">This will make the text easier to read.</span></span>

        ![Police en gras.](images/AzureLabs-Lab1-25.png)

7.  <span data-ttu-id="baf2c-329">Pour chaque *textuel de l’interface utilisateur* créé dans [chapitre 5](#chapter-5--create-the-results-class), créez un *enfant* **textuel de l’interface utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-329">For each *UI Text object* created in [Chapter 5](#chapter-5--create-the-results-class), create a new *child* **UI Text object**.</span></span> <span data-ttu-id="baf2c-330">Ces enfants affiche la sortie de l’application.</span><span class="sxs-lookup"><span data-stu-id="baf2c-330">These children will display the output of the application.</span></span> <span data-ttu-id="baf2c-331">Créer *enfant* objets par clic droit sur votre parent souhaité (par exemple, *MicrophoneStatusLabel*), puis sélectionnez **l’interface utilisateur** , puis sélectionnez **texte**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-331">Create *child* objects through right-clicking your intended parent (e.g. *MicrophoneStatusLabel*) and then select **UI** and then select **Text**.</span></span>
8.  <span data-ttu-id="baf2c-332">Pour chacun de ces enfants, sélectionnez-le et utilisez les tableaux pour définir les paramètres dans le panneau d’inspecteur suivants.</span><span class="sxs-lookup"><span data-stu-id="baf2c-332">For each of these children, select it and use the below tables to set the parameters in the Inspector Panel.</span></span>

    1. <span data-ttu-id="baf2c-333">Pour le **Rect transformation** composant :</span><span class="sxs-lookup"><span data-stu-id="baf2c-333">For the **Rect Transform** component:</span></span>

        | <span data-ttu-id="baf2c-334">Nom</span><span class="sxs-lookup"><span data-stu-id="baf2c-334">Name</span></span>                  | <span data-ttu-id="baf2c-335">Transformer - *Position*</span><span class="sxs-lookup"><span data-stu-id="baf2c-335">Transform - *Position*</span></span> | <span data-ttu-id="baf2c-336">Largeur</span><span class="sxs-lookup"><span data-stu-id="baf2c-336">Width</span></span>      | <span data-ttu-id="baf2c-337">Hauteur</span><span class="sxs-lookup"><span data-stu-id="baf2c-337">Height</span></span>    |
        |:---------------------:|:----------------------:|:----------:|:---------:|
        | <span data-ttu-id="baf2c-338">MicrophoneStatusText</span><span class="sxs-lookup"><span data-stu-id="baf2c-338">MicrophoneStatusText</span></span>  | <span data-ttu-id="baf2c-339">X 0 Y -30 Z 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-339">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="baf2c-340">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-340">300</span></span>        | <span data-ttu-id="baf2c-341">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-341">30</span></span>        |
        | <span data-ttu-id="baf2c-342">AzureResponseText</span><span class="sxs-lookup"><span data-stu-id="baf2c-342">AzureResponseText</span></span>     | <span data-ttu-id="baf2c-343">X 0 Y -30 Z 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-343">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="baf2c-344">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-344">300</span></span>        | <span data-ttu-id="baf2c-345">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-345">30</span></span>        |
        | <span data-ttu-id="baf2c-346">DictationText</span><span class="sxs-lookup"><span data-stu-id="baf2c-346">DictationText</span></span>         | <span data-ttu-id="baf2c-347">X 0 Y -30 Z 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-347">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="baf2c-348">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-348">300</span></span>        | <span data-ttu-id="baf2c-349">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-349">30</span></span>        |
        | <span data-ttu-id="baf2c-350">TranslationResultText</span><span class="sxs-lookup"><span data-stu-id="baf2c-350">TranslationResultText</span></span> | <span data-ttu-id="baf2c-351">X 0 Y -30 Z 0</span><span class="sxs-lookup"><span data-stu-id="baf2c-351">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="baf2c-352">300</span><span class="sxs-lookup"><span data-stu-id="baf2c-352">300</span></span>        | <span data-ttu-id="baf2c-353">30</span><span class="sxs-lookup"><span data-stu-id="baf2c-353">30</span></span>        |

    2. <span data-ttu-id="baf2c-354">Pour le **texte (Script)** composant :</span><span class="sxs-lookup"><span data-stu-id="baf2c-354">For the **Text (Script)** component:</span></span>

        | <span data-ttu-id="baf2c-355">Nom</span><span class="sxs-lookup"><span data-stu-id="baf2c-355">Name</span></span>                  | <span data-ttu-id="baf2c-356">Text</span><span class="sxs-lookup"><span data-stu-id="baf2c-356">Text</span></span>          | <span data-ttu-id="baf2c-357">Taille de police</span><span class="sxs-lookup"><span data-stu-id="baf2c-357">Font Size</span></span>    |
        |:---------------------:|:-------------:|:------------:|
        | <span data-ttu-id="baf2c-358">MicrophoneStatusText</span><span class="sxs-lookup"><span data-stu-id="baf2c-358">MicrophoneStatusText</span></span>  |      <span data-ttu-id="baf2c-359">??</span><span class="sxs-lookup"><span data-stu-id="baf2c-359">??</span></span>       | <span data-ttu-id="baf2c-360">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-360">20</span></span>           |
        | <span data-ttu-id="baf2c-361">AzureResponseText</span><span class="sxs-lookup"><span data-stu-id="baf2c-361">AzureResponseText</span></span>     |      <span data-ttu-id="baf2c-362">??</span><span class="sxs-lookup"><span data-stu-id="baf2c-362">??</span></span>       | <span data-ttu-id="baf2c-363">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-363">20</span></span>           |
        | <span data-ttu-id="baf2c-364">DictationText</span><span class="sxs-lookup"><span data-stu-id="baf2c-364">DictationText</span></span>         |      <span data-ttu-id="baf2c-365">??</span><span class="sxs-lookup"><span data-stu-id="baf2c-365">??</span></span>       | <span data-ttu-id="baf2c-366">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-366">20</span></span>           |
        | <span data-ttu-id="baf2c-367">TranslationResultText</span><span class="sxs-lookup"><span data-stu-id="baf2c-367">TranslationResultText</span></span> |      <span data-ttu-id="baf2c-368">??</span><span class="sxs-lookup"><span data-stu-id="baf2c-368">??</span></span>       | <span data-ttu-id="baf2c-369">20</span><span class="sxs-lookup"><span data-stu-id="baf2c-369">20</span></span>           |

9. <span data-ttu-id="baf2c-370">Ensuite, sélectionnez l’option d’alignement « centre » pour chaque composant de texte :</span><span class="sxs-lookup"><span data-stu-id="baf2c-370">Next, select the 'centre' alignment option for each text component:</span></span>

    ![Aligner le texte.](images/AzureLabs-Lab1-26.png)

10. <span data-ttu-id="baf2c-372">Pour garantir la **enfant textes d’interface utilisateur** objets sont facilement lisibles, modifier leur *couleur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-372">To ensure the **child UI Text** objects are easily readable, change their *Color*.</span></span> <span data-ttu-id="baf2c-373">Cela en cliquant sur la barre (actuellement « noir ») en regard *couleur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-373">Do this by clicking on the bar (currently ‘Black’) next to *Color*.</span></span> 

    ![D’entrée correspondant des valeurs pour les sorties de texte de l’interface utilisateur.](images/AzureLabs-Lab1-27.png)
 
11. <span data-ttu-id="baf2c-375">Ensuite, dans le nouveau, peu, *couleur* fenêtre, de modifier le *couleur hexadécimale* à : **0032EAFF**</span><span class="sxs-lookup"><span data-stu-id="baf2c-375">Then, in the new, little, *Color* window, change the *Hex Color* to: **0032EAFF**</span></span>

    ![Mettre à jour de la couleur bleue.](images/AzureLabs-Lab1-28.png)
 
12. <span data-ttu-id="baf2c-377">Voici comment la **l’interface utilisateur** doit se présenter.</span><span class="sxs-lookup"><span data-stu-id="baf2c-377">Below is how the **UI** should look.</span></span>
    1.  <span data-ttu-id="baf2c-378">Dans le *hiérarchie panneau*:</span><span class="sxs-lookup"><span data-stu-id="baf2c-378">In the *Hierarchy Panel*:</span></span>

        ![Avoir hiérarchie dans la structure fournie.](images/AzureLabs-Lab1-29.png)

    2.  <span data-ttu-id="baf2c-380">Dans le *scène* et *jeux vues*:</span><span class="sxs-lookup"><span data-stu-id="baf2c-380">In the *Scene* and *Game Views*:</span></span>

        ![Avoir les vues de la scène et le jeu dans la même structure.](images/AzureLabs-Lab1-30.png)

## <a name="chapter-5--create-the-results-class"></a><span data-ttu-id="baf2c-382">Chapitre 5 : créer la classe de résultats</span><span class="sxs-lookup"><span data-stu-id="baf2c-382">Chapter 5 – Create the Results class</span></span>

<span data-ttu-id="baf2c-383">Est le premier script que vous avez besoin pour créer le *résultats* (classe), qui est chargé de fournir un moyen pour afficher les résultats de la traduction.</span><span class="sxs-lookup"><span data-stu-id="baf2c-383">The first script you need to create is the *Results* class, which is responsible for providing a way to see the results of translation.</span></span> <span data-ttu-id="baf2c-384">La classe stocke et affiche les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="baf2c-384">The Class stores and displays the following:</span></span> 

- <span data-ttu-id="baf2c-385">Le résultat de la réponse à partir d’Azure.</span><span class="sxs-lookup"><span data-stu-id="baf2c-385">The response result from Azure.</span></span>
- <span data-ttu-id="baf2c-386">L’état du microphone.</span><span class="sxs-lookup"><span data-stu-id="baf2c-386">The microphone status.</span></span> 
- <span data-ttu-id="baf2c-387">Le résultat de la dictée (voix en texte).</span><span class="sxs-lookup"><span data-stu-id="baf2c-387">The result of the dictation (voice to text).</span></span>
- <span data-ttu-id="baf2c-388">Le résultat de la traduction.</span><span class="sxs-lookup"><span data-stu-id="baf2c-388">The result of the translation.</span></span>

<span data-ttu-id="baf2c-389">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-389">To create this class:</span></span> 

1.  <span data-ttu-id="baf2c-390">Avec le bouton droit dans le *Panneau de configuration de projet*, puis **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-390">Right-click in the *Project Panel*, then **Create > Folder**.</span></span> <span data-ttu-id="baf2c-391">Nommez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-391">Name the folder **Scripts**.</span></span> 
 
    ![Créez le dossier scripts.](images/AzureLabs-Lab1-31.png)

    ![Ouvrez le dossier scripts.](images/AzureLabs-Lab1-32.png)
 
2.  <span data-ttu-id="baf2c-394">Avec le **Scripts** créer de dossier, double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="baf2c-394">With the **Scripts** folder create, double click it to open.</span></span> <span data-ttu-id="baf2c-395">Ensuite, dans ce dossier, avec le bouton droit, puis sélectionnez **créer >** puis  **C# Script**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-395">Then within that folder, right-click, and select **Create >** then **C# Script**.</span></span> <span data-ttu-id="baf2c-396">Nommez le script *résultats*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-396">Name the script *Results*.</span></span> 

    ![Créer le premier script.](images/AzureLabs-Lab1-33.png)
 
3.  <span data-ttu-id="baf2c-398">Double-cliquez sur le nouveau *résultats* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-398">Double click on the new *Results* script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="baf2c-399">Insérer des espaces de noms suivants :</span><span class="sxs-lookup"><span data-stu-id="baf2c-399">Insert the following namespaces:</span></span>

    ```cs
        using UnityEngine;
        using UnityEngine.UI;
    ```

5.  <span data-ttu-id="baf2c-400">À l’intérieur de la classe, insérez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="baf2c-400">Inside the Class insert the following variables:</span></span>

    ```cs
        public static Results instance;
   
        [HideInInspector] 
        public string azureResponseCode;
   
        [HideInInspector] 
        public string translationResult;
   
        [HideInInspector] 
        public string dictationResult;
   
        [HideInInspector] 
        public string micStatus;
   
        public Text microphoneStatusText;
   
        public Text azureResponseText;
   
        public Text dictationText;
   
        public Text translationResultText;
    ```

6.  <span data-ttu-id="baf2c-401">Ajoutez ensuite le *Awake()* (méthode), qui sera appelée lors de l’initialisation de la classe.</span><span class="sxs-lookup"><span data-stu-id="baf2c-401">Then add the *Awake()* method, which will be called when the class initializes.</span></span> 

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton 
            instance = this;           
        } 
    ```

7.  <span data-ttu-id="baf2c-402">Enfin, ajoutez les méthodes qui sont responsables de sortir les informations des résultats différents à l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="baf2c-402">Finally, add the methods which are responsible for outputting the various results information to the UI.</span></span> 

    ```csharp
        /// <summary>
        /// Stores the Azure response value in the static instance of Result class.
        /// </summary>
        public void SetAzureResponse(string result)
        {
            azureResponseCode = result;
            azureResponseText.text = azureResponseCode;
        }
   
        /// <summary>
        /// Stores the translated result from dictation in the static instance of Result class. 
        /// </summary>
        public void SetDictationResult(string result)
        {
            dictationResult = result;
            dictationText.text = dictationResult;
        }
   
        /// <summary>
        /// Stores the translated result from Azure Service in the static instance of Result class. 
        /// </summary>
        public void SetTranslatedResult(string result)
        {
            translationResult = result;
            translationResultText.text = translationResult;
        }
   
        /// <summary>
        /// Stores the status of the Microphone in the static instance of Result class. 
        /// </summary>
        public void SetMicrophoneStatus(string result)
        {
            micStatus = result;
            microphoneStatusText.text = micStatus;
        }
    ```

8.  <span data-ttu-id="baf2c-403">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-403">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-6--create-the-microphonemanager-class"></a><span data-ttu-id="baf2c-404">Chapitre 6 : créer le *MicrophoneManager* classe</span><span class="sxs-lookup"><span data-stu-id="baf2c-404">Chapter 6 – Create the *MicrophoneManager* class</span></span>

<span data-ttu-id="baf2c-405">La deuxième classe que vous vous apprêtez à créer est le *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-405">The second class you are going to create is the *MicrophoneManager*.</span></span>

<span data-ttu-id="baf2c-406">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="baf2c-406">This class is responsible for:</span></span>

- <span data-ttu-id="baf2c-407">Détection du périphérique d’enregistrement attaché à l’ordinateur (selon celui qui est la valeur par défaut) ou un casque.</span><span class="sxs-lookup"><span data-stu-id="baf2c-407">Detecting the recording device attached to the headset or machine (whichever is the default).</span></span>
- <span data-ttu-id="baf2c-408">Capturer l’audio (voix) et la dictée pour stocker en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="baf2c-408">Capture the audio (voice) and use dictation to store it as a string.</span></span>
- <span data-ttu-id="baf2c-409">Une fois que la voix a été suspendu, soumettez la dictée pour la classe de convertisseur.</span><span class="sxs-lookup"><span data-stu-id="baf2c-409">Once the voice has paused, submit the dictation to the Translator class.</span></span>
- <span data-ttu-id="baf2c-410">Héberger une méthode qui peut arrêter la capture vocale si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="baf2c-410">Host a method that can stop the voice capture if desired.</span></span>

<span data-ttu-id="baf2c-411">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-411">To create this class:</span></span> 
1.  <span data-ttu-id="baf2c-412">Double-cliquez sur le **Scripts** dossier, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="baf2c-412">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="baf2c-413">Avec le bouton droit à l’intérieur de la **Scripts** dossier, cliquez sur **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-413">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="baf2c-414">Nommez le script *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-414">Name the script *MicrophoneManager*.</span></span> 
3.  <span data-ttu-id="baf2c-415">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="baf2c-415">Double click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="baf2c-416">Mettre à jour les espaces de noms pour être le même que la commande suivante, en haut de la *MicrophoneManager* classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-416">Update the namespaces to be the same as the following, at the top of the *MicrophoneManager* class:</span></span>

    ```csharp
        using UnityEngine; 
        using UnityEngine.Windows.Speech;
    ```

5.  <span data-ttu-id="baf2c-417">Ensuite, ajoutez les variables suivantes à l’intérieur de la *MicrophoneManager* classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-417">Then, add the following variables inside the *MicrophoneManager* class:</span></span>

    ```csharp
        // Help to access instance of this object 
        public static MicrophoneManager instance; 
     
        // AudioSource component, provides access to mic 
        private AudioSource audioSource; 
   
        // Flag indicating mic detection 
        private bool microphoneDetected; 
   
        // Component converting speech to text 
        private DictationRecognizer dictationRecognizer; 
    ```

6.  <span data-ttu-id="baf2c-418">Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="baf2c-418">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="baf2c-419">Il seront appelées lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-419">These will be called when the class initializes:</span></span>

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton 
            instance = this; 
        } 
    
        void Start() 
        { 
            //Use Unity Microphone class to detect devices and setup AudioSource 
            if(Microphone.devices.Length > 0) 
            { 
                Results.instance.SetMicrophoneStatus("Initialising..."); 
                audioSource = GetComponent<AudioSource>(); 
                microphoneDetected = true; 
            } 
            else 
            { 
                Results.instance.SetMicrophoneStatus("No Microphone detected"); 
            } 
        } 
    ```

7.  <span data-ttu-id="baf2c-420">Vous pouvez *supprimer* le *Update()* étant donné que cette classe ne l’utilise pas de méthode.</span><span class="sxs-lookup"><span data-stu-id="baf2c-420">You can *delete* the *Update()* method since this class will not use it.</span></span>
8.  <span data-ttu-id="baf2c-421">Maintenant, vous devez les méthodes que l’application utilise pour démarrer et arrêter la capture de la voix et transmettez-le à la *Translator* (classe), que vous allez générer plus rapidement.</span><span class="sxs-lookup"><span data-stu-id="baf2c-421">Now you need the methods that the App uses to start and stop the voice capture, and pass it to the *Translator* class, that you will build soon.</span></span> <span data-ttu-id="baf2c-422">Copiez le code suivant et collez-le sous la *Start()* (méthode).</span><span class="sxs-lookup"><span data-stu-id="baf2c-422">Copy the following code and paste it beneath the *Start()* method.</span></span>

    ```csharp
        /// <summary> 
        /// Start microphone capture. Debugging message is delivered to the Results class. 
        /// </summary> 
        public void StartCapturingAudio() 
        { 
            if(microphoneDetected) 
            {               
                // Start dictation 
                dictationRecognizer = new DictationRecognizer(); 
                dictationRecognizer.DictationResult += DictationRecognizer_DictationResult; 
                dictationRecognizer.Start(); 
    
                // Update UI with mic status 
                Results.instance.SetMicrophoneStatus("Capturing..."); 
            }      
        } 
 
        /// <summary> 
        /// Stop microphone capture. Debugging message is delivered to the Results class. 
        /// </summary> 
        public void StopCapturingAudio() 
        { 
            Results.instance.SetMicrophoneStatus("Mic sleeping"); 
            Microphone.End(null); 
            dictationRecognizer.DictationResult -= DictationRecognizer_DictationResult; 
            dictationRecognizer.Dispose(); 
        }
    ```

    > [!TIP]
    > <span data-ttu-id="baf2c-423">Bien que cette application ne fera pas l’utiliser, le *StopCapturingAudio()* méthode a également été fournie ici, si vous souhaitez implémenter la possibilité d’arrêter la capture audio dans votre application.</span><span class="sxs-lookup"><span data-stu-id="baf2c-423">Though this application will not make use of it, the *StopCapturingAudio()* method has also been provided here, should you want to implement the ability to stop capturing audio in your application.</span></span>

9.  <span data-ttu-id="baf2c-424">Vous devez maintenant ajouter un gestionnaire de dictée qui sera appelé lorsque la voix s’arrête.</span><span class="sxs-lookup"><span data-stu-id="baf2c-424">You now need to add a Dictation Handler that will be invoked when the voice stops.</span></span> <span data-ttu-id="baf2c-425">Cette méthode passe ensuite le texte dicté à la *Translator* classe.</span><span class="sxs-lookup"><span data-stu-id="baf2c-425">This method will then pass the dictated text to the *Translator* class.</span></span>

    ```csharp
        /// <summary>
        /// This handler is called every time the Dictation detects a pause in the speech. 
        /// Debugging message is delivered to the Results class.
        /// </summary>
        private void DictationRecognizer_DictationResult(string text, ConfidenceLevel confidence)
        {
            // Update UI with dictation captured
            Results.instance.SetDictationResult(text);
   
            // Start the coroutine that process the dictation through Azure 
            StartCoroutine(Translator.instance.TranslateWithUnityNetworking(text));   
        }
    ```

10. <span data-ttu-id="baf2c-426">Veillez à enregistrer vos modifications dans Visual Studio avant de retourner à Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-426">Be sure to save your changes in Visual Studio before returning to Unity.</span></span>

> [!WARNING]  
> <span data-ttu-id="baf2c-427">À ce stade, vous remarquerez une erreur qui apparaissent dans le *Console de l’éditeur Unity* panneau (« le nom « Translator » n’existe pas... »).</span><span class="sxs-lookup"><span data-stu-id="baf2c-427">At this point you will notice an error appearing in the *Unity Editor Console* Panel (“The name ‘Translator’ does not exist...”).</span></span> <span data-ttu-id="baf2c-428">Il s’agit, car le code fait référence le *Translator* (classe), que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="baf2c-428">This is because the code references the *Translator* class, which you will create in the next chapter.</span></span>

## <a name="chapter-7--call-to-azure-and-translator-service"></a><span data-ttu-id="baf2c-429">Chapitre 7 – appel au service Azure et translator</span><span class="sxs-lookup"><span data-stu-id="baf2c-429">Chapter 7 – Call to Azure and translator service</span></span>

<span data-ttu-id="baf2c-430">Est le dernier script, vous devez créer le *Translator* classe.</span><span class="sxs-lookup"><span data-stu-id="baf2c-430">The last script you need to create is the *Translator* class.</span></span> 

<span data-ttu-id="baf2c-431">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="baf2c-431">This class is responsible for:</span></span>

-   <span data-ttu-id="baf2c-432">L’authentification de l’application avec *Azure*, exchange pour un **du jeton d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-432">Authenticating the App with *Azure*, in exchange for an **Auth Token**.</span></span>
-   <span data-ttu-id="baf2c-433">Utilisez le **du jeton d’authentification** pour envoyer du texte (reçus à partir de la *MicrophoneManager* classe) à traduire.</span><span class="sxs-lookup"><span data-stu-id="baf2c-433">Use the **Auth Token** to submit text (received from the *MicrophoneManager* Class) to be translated.</span></span>
-   <span data-ttu-id="baf2c-434">Recevoir le résultat traduit et transmettez-le à la *résultats* classe à visualiser dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="baf2c-434">Receive the translated result and pass it to the *Results* Class to be visualized in the UI.</span></span>

<span data-ttu-id="baf2c-435">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-435">To create this Class:</span></span> 
1.  <span data-ttu-id="baf2c-436">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="baf2c-436">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="baf2c-437">Avec le bouton droit dans le **Panneau de configuration de projet**, **créer > C# Script**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-437">Right-click in the **Project Panel**, **Create > C# Script**.</span></span> <span data-ttu-id="baf2c-438">Appeler le script *Translator*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-438">Call the script *Translator*.</span></span>
3.  <span data-ttu-id="baf2c-439">Double-cliquez sur le nouveau *Translator* script pour l’ouvrir **avec Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-439">Double click on the new *Translator* script to open it **with Visual Studio**.</span></span>
4.  <span data-ttu-id="baf2c-440">Ajoutez les espaces de noms suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="baf2c-440">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Xml.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="baf2c-441">Puis ajoutez les variables suivantes à l’intérieur de la *Translator* classe :</span><span class="sxs-lookup"><span data-stu-id="baf2c-441">Then add the following variables inside the *Translator* class:</span></span>

    ```csharp
        public static Translator instance; 
        private string translationTokenEndpoint = "https://api.cognitive.microsoft.com/sts/v1.0/issueToken"; 
        private string translationTextEndpoint = "https://api.microsofttranslator.com/v2/http.svc/Translate?"; 
        private const string ocpApimSubscriptionKeyHeader = "Ocp-Apim-Subscription-Key"; 
    
        //Substitute the value of authorizationKey with your own Key 
        private const string authorizationKey = "-InsertYourAuthKeyHere-"; 
        private string authorizationToken; 
    
        // languages set below are: 
        // English 
        // French 
        // Italian 
        // Japanese 
        // Korean 
        public enum Languages { en, fr, it, ja, ko }; 
        public Languages from = Languages.en; 
        public Languages to = Languages.it; 
    ```

    > [!NOTE]
    > - <span data-ttu-id="baf2c-442">Les langues insérées dans les langues **enum** sont de simples exemples.</span><span class="sxs-lookup"><span data-stu-id="baf2c-442">The languages inserted into the languages **enum** are just examples.</span></span> <span data-ttu-id="baf2c-443">Vous pouvez ajouter plus si vous le souhaitez ; le [API prend en charge plus de 60 langues](https://docs.microsoft.com/azure/cognitive-services/translator/languages) (y compris Klingon) !</span><span class="sxs-lookup"><span data-stu-id="baf2c-443">Feel free to add more if you wish; the [API supports over 60 languages](https://docs.microsoft.com/azure/cognitive-services/translator/languages) (including Klingon)!</span></span>
    > - <span data-ttu-id="baf2c-444">Est un [page plus interactive sur des langages disponibles](https://www.microsoft.com/translator/business/languages/), sachez cependant à la page s’affiche uniquement pour fonctionner lorsque la langue du site est définie sur « en-us (et le site de Microsoft sera probablement rediriger vers votre langue maternelle).</span><span class="sxs-lookup"><span data-stu-id="baf2c-444">There is a [more interactive page covering available languages](https://www.microsoft.com/translator/business/languages/), though be aware the page only appears to work when the site language is set to 'en-us' (and the Microsoft site will likely redirect to your native language).</span></span> <span data-ttu-id="baf2c-445">Vous pouvez modifier la langue du site au bas de la page ou en modifiant l’URL.</span><span class="sxs-lookup"><span data-stu-id="baf2c-445">You can change site language at the bottom of the page or by altering the URL.</span></span>
    > - <span data-ttu-id="baf2c-446">Le **authorizationKey** valeur, dans l’extrait de code ci-dessus, doit être le **clé** que vous avez reçu lors de votre abonnement à la *Azure l’API Translator Text*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-446">The **authorizationKey** value, in the above code snippet, must be the **Key**  you received when you subscribed to the *Azure Translator Text API*.</span></span> <span data-ttu-id="baf2c-447">Cela a été couvert dans [chapitre 1](#chapter-1--the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="baf2c-447">This was covered in [Chapter 1](#chapter-1--the-azure-portal).</span></span>

6.  <span data-ttu-id="baf2c-448">Code pour le *Awake()* et *Start()* méthodes doit maintenant être ajouté.</span><span class="sxs-lookup"><span data-stu-id="baf2c-448">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span> 
7.  <span data-ttu-id="baf2c-449">Dans ce cas, le code effectue un appel à *Azure* à l’aide de l’autorisation de clé, pour obtenir un *jeton*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-449">In this case, the code will make a call to *Azure* using the authorization Key, to get a *Token*.</span></span>

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton  
            instance = this; 
        } 
    
        // Use this for initialization  
        void Start() 
        { 
            // When the application starts, request an auth token 
            StartCoroutine("GetTokenCoroutine", authorizationKey); 
        }
    ```

    > [!NOTE]
    > <span data-ttu-id="baf2c-450">Le jeton expire après 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="baf2c-450">The token will expire after 10 minutes.</span></span> <span data-ttu-id="baf2c-451">Selon le scénario de votre application, vous devrez peut-être rendre la coroutine même appeler plusieurs fois.</span><span class="sxs-lookup"><span data-stu-id="baf2c-451">Depending on the scenario for your app, you might have to make the same coroutine call multiple times.</span></span>

8.  <span data-ttu-id="baf2c-452">La coroutine pour obtenir le jeton est la suivante :</span><span class="sxs-lookup"><span data-stu-id="baf2c-452">The coroutine to obtain the Token is the following:</span></span>

    ```csharp
        /// <summary> 
        /// Request a Token from Azure Translation Service by providing the access key. 
        /// Debugging result is delivered to the Results class. 
        /// </summary> 
        private IEnumerator GetTokenCoroutine(string key)
        {
            if (string.IsNullOrEmpty(key))
            {
                throw new InvalidOperationException("Authorization key not set.");
            }

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(translationTokenEndpoint, string.Empty))
            {
                unityWebRequest.SetRequestHeader("Ocp-Apim-Subscription-Key", key);
                yield return unityWebRequest.SendWebRequest();

                long responseCode = unityWebRequest.responseCode;

                // Update the UI with the response code 
                Results.instance.SetAzureResponse(responseCode.ToString());

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Results.instance.azureResponseText.text = unityWebRequest.error;
                    yield return null;
                }
                else
                {
                    authorizationToken = unityWebRequest.downloadHandler.text;
                }
            }

            // After receiving the token, begin capturing Audio with the MicrophoneManager Class 
            MicrophoneManager.instance.StartCapturingAudio();
        }
    ```

    > [!WARNING]
    > <span data-ttu-id="baf2c-453">Si vous modifiez le nom de la méthode IEnumerator **GetTokenCoroutine()**, vous devez mettre à jour le *StartCoroutine* et *StopCoroutine* appeler des valeurs de chaîne dans le code ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="baf2c-453">If you edit the name of the IEnumerator method **GetTokenCoroutine()**, you need to update the *StartCoroutine* and *StopCoroutine* call string values in the above code.</span></span> <span data-ttu-id="baf2c-454">[Selon la documentation Unity](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StartCoroutine.html), pour arrêter un spécifique *Coroutine*, vous devez utiliser la méthode de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="baf2c-454">[As per Unity documentation](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StartCoroutine.html), to Stop a specific *Coroutine*, you need to use the string value method.</span></span>

9.  <span data-ttu-id="baf2c-455">Ensuite, ajoutez la coroutine (avec une méthode de flux « support » juste en dessous) pour obtenir la traduction du texte reçue par le *MicrophoneManager* classe.</span><span class="sxs-lookup"><span data-stu-id="baf2c-455">Next, add the coroutine (with a “support” stream method right below it) to obtain the translation of the text received by the *MicrophoneManager* class.</span></span> <span data-ttu-id="baf2c-456">Ce code crée une chaîne de requête à envoyer à la *Azure l’API Translator Text*, puis utilise la classe Unity UnityWebRequest interne pour effectuer un appel de 'Get' pour le point de terminaison avec la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="baf2c-456">This code creates a query string to send to the *Azure Translator Text API*, and then uses the internal Unity UnityWebRequest class to make a ‘Get’ call to the endpoint with the query string.</span></span> <span data-ttu-id="baf2c-457">Le résultat est ensuite utilisé pour définir la traduction dans votre objet de résultats.</span><span class="sxs-lookup"><span data-stu-id="baf2c-457">The result is then used to set the translation in your Results object.</span></span> <span data-ttu-id="baf2c-458">Le code ci-dessous illustre l’implémentation :</span><span class="sxs-lookup"><span data-stu-id="baf2c-458">The code below shows the implementation:</span></span>

    ```csharp
        /// <summary> 
        /// Request a translation from Azure Translation Service by providing a string.  
        /// Debugging result is delivered to the Results class. 
        /// </summary> 
        public IEnumerator TranslateWithUnityNetworking(string text)
        {
            // This query string will contain the parameters for the translation 
            string queryString = string.Concat("text=", Uri.EscapeDataString(text), "&from=", from, "&to=", to);

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Get(translationTextEndpoint + queryString))
            {
                unityWebRequest.SetRequestHeader("Authorization", "Bearer " + authorizationToken);
                unityWebRequest.SetRequestHeader("Accept", "application/xml");
                yield return unityWebRequest.SendWebRequest();

                if (unityWebRequest.isNetworkError || unityWebRequest.isHttpError)
                {
                    Debug.Log(unityWebRequest.error);
                    yield return null;
                }

                // Parse out the response text from the returned Xml
                string result = XElement.Parse(unityWebRequest.downloadHandler.text).Value;
                Results.instance.SetTranslatedResult(result);
            }
        }
    ```

10. <span data-ttu-id="baf2c-459">Veillez à enregistrer vos modifications dans *Visual Studio* avant de retourner à *Unity*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-459">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8--configure-the-unity-scene"></a><span data-ttu-id="baf2c-460">Chapitre 8 : configurer la scène Unity</span><span class="sxs-lookup"><span data-stu-id="baf2c-460">Chapter 8 – Configure the Unity Scene</span></span>

1.  <span data-ttu-id="baf2c-461">Précédent dans l’éditeur Unity, cliquez et faites glisser le *résultats* classe *à partir de* le **Scripts** dossier pour le **Main Camera** objet dans le  *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-461">Back in the Unity Editor, click and drag the *Results* class *from* the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
2.  <span data-ttu-id="baf2c-462">Cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-462">Click on the **Main Camera** and look at the *Inspector Panel*.</span></span> <span data-ttu-id="baf2c-463">Vous remarquerez que dans récemment ajouté *Script* composant, il existe quatre champs avec des valeurs vides.</span><span class="sxs-lookup"><span data-stu-id="baf2c-463">You will notice that within the newly added *Script* component, there are four fields with empty values.</span></span> <span data-ttu-id="baf2c-464">Voici les références de sortie pour les propriétés dans le code.</span><span class="sxs-lookup"><span data-stu-id="baf2c-464">These are the output references to the properties in the code.</span></span> 
3.  <span data-ttu-id="baf2c-465">Faites glisser le texte approprié **texte** objets à partir de la *hiérarchie panneau* à ces quatre emplacements, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="baf2c-465">Drag the appropriate **Text** objects from the *Hierarchy Panel* to those four slots, as shown in the image below.</span></span>

    ![Mettre à jour les références de la cible avec les valeurs spécifiées.](images/AzureLabs-Lab1-34.png)
  
4.  <span data-ttu-id="baf2c-467">Ensuite, cliquez et faites glisser le *Translator* classe à partir de la **Scripts** dossier pour le **Main Camera** de l’objet dans le *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-467">Next, click and drag the *Translator* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 
5.  <span data-ttu-id="baf2c-468">Ensuite, cliquez et faites glisser le *MicrophoneManager* classe à partir de la **Scripts** dossier à la **Main Camera** de l’objet dans le *Panneau de la hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-468">Then, click and drag the *MicrophoneManager* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 
6.  <span data-ttu-id="baf2c-469">Enfin, cliquez sur le **Main Camera** et examinez le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-469">Lastly, click on the **Main Camera** and look at the *Inspector Panel*.</span></span> <span data-ttu-id="baf2c-470">Vous remarquerez que dans le script que vous avez fait glisser sur, il y a deux listes déroulantes qui vous permet de définir les langues.</span><span class="sxs-lookup"><span data-stu-id="baf2c-470">You will notice that in the script you dragged on, there are two drop down boxes that will allow you to set the languages.</span></span>
 
    ![Vérifiez que les langues de traduction prévue sont entrées.](images/AzureLabs-Lab1-35.png)

## <a name="chapter-9--test-in-mixed-reality"></a><span data-ttu-id="baf2c-472">Chapitre 9 – Test en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="baf2c-472">Chapter 9 – Test in mixed reality</span></span>

<span data-ttu-id="baf2c-473">À ce stade, vous devez tester que la scène a été implémentée correctement.</span><span class="sxs-lookup"><span data-stu-id="baf2c-473">At this point you need to test that the Scene has been properly implemented.</span></span>

<span data-ttu-id="baf2c-474">Vérifiez que :</span><span class="sxs-lookup"><span data-stu-id="baf2c-474">Ensure that:</span></span>

- <span data-ttu-id="baf2c-475">Tous les paramètres mentionnés dans [chapitre 1](#chapter-1--the-azure-portal) sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="baf2c-475">All the settings mentioned in [Chapter 1](#chapter-1--the-azure-portal) are set correctly.</span></span> 
- <span data-ttu-id="baf2c-476">Le *résultats*, *Translator*, et *MicrophoneManager*, les scripts sont attachés à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="baf2c-476">The *Results*, *Translator*, and *MicrophoneManager*, scripts are attached to the **Main Camera** object.</span></span> 
- <span data-ttu-id="baf2c-477">Vous avez placé votre *Azure l’API Translator Text* Service **clé** au sein de la **authorizationKey** variable dans le *Translator* Script.</span><span class="sxs-lookup"><span data-stu-id="baf2c-477">You have placed your *Azure Translator Text API* Service **Key** within the **authorizationKey** variable within the *Translator* Script.</span></span>  
- <span data-ttu-id="baf2c-478">Tous les champs dans le *panneau Inspecteur de caméra principal* sont affectées correctement.</span><span class="sxs-lookup"><span data-stu-id="baf2c-478">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>
- <span data-ttu-id="baf2c-479">Votre microphone fonctionne lors de l’exécution de votre scène (dans le cas contraire, vérifiez que votre microphone attaché est le *par défaut* appareil et que vous avez [configuré correctement dans Windows](https://support.microsoft.com/en-au/help/4027981/windows-how-to-set-up-and-test-microphones-in-windows-10)).</span><span class="sxs-lookup"><span data-stu-id="baf2c-479">Your microphone is working when running your scene (if not, check that your attached microphone is the *default* device, and that you have [set it up correctly within Windows](https://support.microsoft.com/en-au/help/4027981/windows-how-to-set-up-and-test-microphones-in-windows-10)).</span></span>

<span data-ttu-id="baf2c-480">Vous pouvez tester le casque immersif en appuyant sur la **lire** situé dans le *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-480">You can test the immersive headset by pressing the **Play** button in the *Unity Editor*.</span></span>
<span data-ttu-id="baf2c-481">L’application doit fonctionner via le casque immersif attaché.</span><span class="sxs-lookup"><span data-stu-id="baf2c-481">The App should be functioning through the attached immersive headset.</span></span>

> [!WARNING]  
> <span data-ttu-id="baf2c-482">Si vous voyez une erreur dans la console Unity sur le périphérique audio par défaut modification, la scène peut ne pas fonctionne comme prévu.</span><span class="sxs-lookup"><span data-stu-id="baf2c-482">If you see an error in the Unity console about the default audio device changing, the scene may not function as expected.</span></span> <span data-ttu-id="baf2c-483">Cela est dû au mode que microphones intégrés pour les casques qui en sont munis porte sur le portail de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="baf2c-483">This is due to the way the mixed reality portal deals with built-in microphones for headsets that have them.</span></span> <span data-ttu-id="baf2c-484">Si vous cette erreur se produit, simplement arrêtez la scène et démarrez à nouveau et les choses peuvent fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="baf2c-484">If you see this error, simply stop the scene and start it again and things should work as expected.</span></span>

## <a name="chapter-10--build-the-uwp-solution-and-sideload-on-local-machine"></a><span data-ttu-id="baf2c-485">Chapitre 10 – générer la solution UWP et le chargement de version test sur l’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="baf2c-485">Chapter 10 – Build the UWP solution and sideload on local machine</span></span>

<span data-ttu-id="baf2c-486">Tous les éléments nécessaires pour la section Unity de ce projet sont maintenant terminée, il est temps de générer à partir de Unity.</span><span class="sxs-lookup"><span data-stu-id="baf2c-486">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="baf2c-487">Accédez à **les paramètres de génération**: **Fichier > Paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="baf2c-487">Navigate to **Build Settings**: **File > Build Settings...**</span></span>
2.  <span data-ttu-id="baf2c-488">À partir de la **paramètres de Build** fenêtre, cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-488">From the **Build Settings** window, click **Build**.</span></span>

    ![Générer la scène Unity.](images/AzureLabs-Lab1-36.png)
  
3.  <span data-ttu-id="baf2c-490">Si pas déjà fait, cochez **Unity C# projets**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-490">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="baf2c-491">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-491">Click **Build**.</span></span> <span data-ttu-id="baf2c-492">Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="baf2c-492">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="baf2c-493">Créez ce dossier, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-493">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="baf2c-494">Ensuite avec le *application* dossier sélectionné, appuyez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-494">Then with the *App* folder selected, press **Select Folder**.</span></span> 
5.  <span data-ttu-id="baf2c-495">Unity commencera à générer votre projet pour le *application* dossier.</span><span class="sxs-lookup"><span data-stu-id="baf2c-495">Unity will begin building your project to the *App* folder.</span></span> 
6.  <span data-ttu-id="baf2c-496">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un *Explorateur de fichiers* fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="baf2c-496">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-11--deploy-your-application"></a><span data-ttu-id="baf2c-497">Chapitre 11 – déployer votre application</span><span class="sxs-lookup"><span data-stu-id="baf2c-497">Chapter 11 – Deploy your application</span></span>

<span data-ttu-id="baf2c-498">Pour déployer votre application :</span><span class="sxs-lookup"><span data-stu-id="baf2c-498">To deploy your application:</span></span>

1.  <span data-ttu-id="baf2c-499">Accédez à votre nouvelle build Unity (le *application* dossier) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-499">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
2.  <span data-ttu-id="baf2c-500">Dans, sélectionnez la Configuration de Solution **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-500">In the Solution Configuration select **Debug**.</span></span>
3.  <span data-ttu-id="baf2c-501">Dans la plateforme de Solution, sélectionnez **x86**, **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="baf2c-501">In the Solution Platform, select **x86**, **Local Machine**.</span></span> 

    > <span data-ttu-id="baf2c-502">Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="baf2c-502">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="baf2c-503">Cependant, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="baf2c-503">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="baf2c-504">Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="baf2c-504">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="baf2c-505">Vérifiez *Mode développeur* est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="baf2c-505">Ensure *Developer Mode* is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab1-37.png)
    
 
4.  <span data-ttu-id="baf2c-507">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre PC.</span><span class="sxs-lookup"><span data-stu-id="baf2c-507">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your PC.</span></span>
5.  <span data-ttu-id="baf2c-508">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="baf2c-508">Your App should now appear in the list of installed apps, ready to be launched.</span></span>
6.  <span data-ttu-id="baf2c-509">Une fois lancé, l’application vous invite à autoriser l’accès à l’aide du Microphone.</span><span class="sxs-lookup"><span data-stu-id="baf2c-509">Once launched, the App will prompt you to authorize access to the Microphone.</span></span> <span data-ttu-id="baf2c-510">Veillez à cliquer sur le **Oui** bouton.</span><span class="sxs-lookup"><span data-stu-id="baf2c-510">Make sure to click the **YES** button.</span></span>
7.  <span data-ttu-id="baf2c-511">Vous êtes maintenant prêt à commencer à traduire !</span><span class="sxs-lookup"><span data-stu-id="baf2c-511">You are now ready to start translating!</span></span>

## <a name="your-finished-translation-text-api-application"></a><span data-ttu-id="baf2c-512">Votre application API de traduction texte terminée</span><span class="sxs-lookup"><span data-stu-id="baf2c-512">Your finished Translation Text API application</span></span>

<span data-ttu-id="baf2c-513">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de texte de traduction de Azure pour convertissez la parole en texte traduit.</span><span class="sxs-lookup"><span data-stu-id="baf2c-513">Congratulations, you built a mixed reality app that leverages the Azure Translation Text API to convert speech to translated text.</span></span>

![Produit final.](images/AzureLabs-Lab1-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="baf2c-515">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="baf2c-515">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="baf2c-516">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="baf2c-516">Exercise 1</span></span>

<span data-ttu-id="baf2c-517">Pouvez-vous ajouter des fonctionnalités de synthèse vocale à l’application, afin que le texte retourné est lu ?</span><span class="sxs-lookup"><span data-stu-id="baf2c-517">Can you add text-to-speech functionality to the app, so that the returned text is spoken?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="baf2c-518">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="baf2c-518">Exercise 2</span></span>

<span data-ttu-id="baf2c-519">Permettre à l’utilisateur de modifier les langues source et la sortie (« from » et « to ») au sein de l’application elle-même, afin de l’application n’a pas besoin d’être reconstruit chaque fois que vous souhaitez modifier les langues.</span><span class="sxs-lookup"><span data-stu-id="baf2c-519">Make it possible for the user to change the source and output languages ('from' and 'to') within the app itself, so the app does not need to be rebuilt every time you want to change languages.</span></span>
