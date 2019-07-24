---
title: Traduction de m et Azure 301-traduction
description: Suivez ce cours pour apprendre à implémenter le API de traduction de texte Translator Text Azure dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, texte de traducteur, hololens, immersif, VR
ms.openlocfilehash: 6fe31d1bcb72337f0a3e8664893ea0f7c0540aae
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63554337"
---
>[!NOTE]
><span data-ttu-id="7d727-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="7d727-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="7d727-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="7d727-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="7d727-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7d727-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="7d727-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="7d727-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="7d727-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="7d727-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="7d727-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="7d727-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-301-language-translation"></a><span data-ttu-id="7d727-110">MR et Azure 301: Traduction linguistique</span><span class="sxs-lookup"><span data-stu-id="7d727-110">MR and Azure 301: Language translation</span></span>

<span data-ttu-id="7d727-111">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de traduction à une application de réalité mixte à l’aide d’Azure Cognitive Services, avec la API de traduction de texte Translator Text.</span><span class="sxs-lookup"><span data-stu-id="7d727-111">In this course, you will learn how to add translation capabilities to a mixed reality application using Azure Cognitive Services, with the Translator Text API.</span></span>

![Produit final](images/AzureLabs-Lab1-00.png)

<span data-ttu-id="7d727-113">Le API de traduction de texte Translator Text est un service de traduction qui fonctionne quasiment en temps réel.</span><span class="sxs-lookup"><span data-stu-id="7d727-113">The Translator Text API is a translation Service which works in near real-time.</span></span> <span data-ttu-id="7d727-114">Le service est basé sur le Cloud et, à l’aide d’un appel d’API REST, une application peut utiliser la technologie de traduction d’ordinateur neuronal pour traduire du texte dans une autre langue.</span><span class="sxs-lookup"><span data-stu-id="7d727-114">The Service is cloud-based, and, using a REST API call, an app can make use of the neural machine translation technology to translate text to another language.</span></span> <span data-ttu-id="7d727-115">Pour plus d’informations, consultez la [page API de traduction de texte Translator Text Azure](https://azure.microsoft.com/services/cognitive-services/translator-text-api/).</span><span class="sxs-lookup"><span data-stu-id="7d727-115">For more information, visit the [Azure Translator Text API page](https://azure.microsoft.com/services/cognitive-services/translator-text-api/).</span></span>

<span data-ttu-id="7d727-116">À la fin de ce cours, vous disposerez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d727-116">Upon completion of this course, you will have a mixed reality application which will be able to do the following:</span></span>

1.  <span data-ttu-id="7d727-117">L’utilisateur se prononcera dans un microphone connecté à un casque immersif (ou au microphone intégré de HoloLens).</span><span class="sxs-lookup"><span data-stu-id="7d727-117">The user will speak into a microphone connected to an immersive (VR) headset (or the built-in microphone of HoloLens).</span></span>
2.  <span data-ttu-id="7d727-118">L’application capture la dictée et l’envoie au API de traduction de texte Translator Text Azure.</span><span class="sxs-lookup"><span data-stu-id="7d727-118">The app will capture the dictation and send it to the Azure Translator Text API.</span></span>
3.  <span data-ttu-id="7d727-119">Le résultat de la traduction s’affiche dans un groupe d’interface utilisateur simple dans la scène Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-119">The translation result will be displayed in a simple UI group in the Unity Scene.</span></span>

<span data-ttu-id="7d727-120">Ce cours vous apprend à obtenir les résultats du service de traduction dans un exemple d’application à base d’Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-120">This course will teach you how to get the results from the Translator Service into a Unity-based sample application.</span></span> <span data-ttu-id="7d727-121">Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.</span><span class="sxs-lookup"><span data-stu-id="7d727-121">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="7d727-122">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="7d727-122">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="7d727-123">Course</span><span class="sxs-lookup"><span data-stu-id="7d727-123">Course</span></span></th><th style="width:150px"> <span data-ttu-id="7d727-124"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="7d727-124"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="7d727-125"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="7d727-125"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="7d727-126">MR et Azure 301: Traduction linguistique</span><span class="sxs-lookup"><span data-stu-id="7d727-126">MR and Azure 301: Language translation</span></span></td><td style="text-align: center;"> <span data-ttu-id="7d727-127">✔️</span><span class="sxs-lookup"><span data-stu-id="7d727-127">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="7d727-128">✔️</span><span class="sxs-lookup"><span data-stu-id="7d727-128">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="7d727-129">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7d727-129">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="7d727-130">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="7d727-130">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="7d727-131">Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="7d727-131">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7d727-132">Prérequis</span><span class="sxs-lookup"><span data-stu-id="7d727-132">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="7d727-133">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="7d727-133">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="7d727-134">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="7d727-134">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="7d727-135">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d727-135">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="7d727-136">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="7d727-136">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="7d727-137">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="7d727-137">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="7d727-138">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="7d727-138">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7d727-139">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="7d727-139">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7d727-140">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="7d727-140">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="7d727-141">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7d727-141">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="7d727-142">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="7d727-142">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="7d727-143">Un jeu de casque avec un microphone intégré (si le casque n’a pas de MIC et de haut-parleurs intégrés)</span><span class="sxs-lookup"><span data-stu-id="7d727-143">A set of headphones with a built-in microphone (if the headset doesn't have a built-in mic and speakers)</span></span>
- <span data-ttu-id="7d727-144">Accès à Internet pour la configuration d’Azure et la récupération des traductions</span><span class="sxs-lookup"><span data-stu-id="7d727-144">Internet access for Azure setup and translation retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="7d727-145">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="7d727-145">Before you start</span></span>

- <span data-ttu-id="7d727-146">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="7d727-146">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
- <span data-ttu-id="7d727-147">Le code de ce didacticiel vous permet d’enregistrer à partir du périphérique microphone par défaut connecté à votre PC.</span><span class="sxs-lookup"><span data-stu-id="7d727-147">The code in this tutorial will allow you to record from the default microphone device connected to your PC.</span></span> <span data-ttu-id="7d727-148">Assurez-vous que le périphérique microphone par défaut est défini sur l’appareil que vous prévoyez d’utiliser pour capturer votre voix.</span><span class="sxs-lookup"><span data-stu-id="7d727-148">Make sure the default microphone device is set to the device you plan to use to capture your voice.</span></span>
- <span data-ttu-id="7d727-149">Pour permettre à votre PC d’activer la dictée, accédez à **paramètres > confidentialité > reconnaissance vocale, entrée manuscrite & frappe** et sélectionnez le bouton **activer les services vocaux et les suggestions de saisie**.</span><span class="sxs-lookup"><span data-stu-id="7d727-149">To allow your PC to enable dictation, go to **Settings > Privacy > Speech, inking & typing** and select the button **Turn On speech services and typing suggestions**.</span></span>
- <span data-ttu-id="7d727-150">Si vous utilisez un microphone et un casque connectés à votre casque (ou intégrés à celui-ci), assurez-vous que l’option «lors de l’usure du casque, basculez vers casque MIC» est activée dans **paramètres > réalité mixte > audio et discours**.</span><span class="sxs-lookup"><span data-stu-id="7d727-150">If you're using a microphone and headphones connected to (or built-in to) your headset, make sure the option “When I wear my headset, switch to headset mic” is turned on in **Settings > Mixed reality > Audio and speech**.</span></span>

   ![Paramètres de réalité mixte](images/AzureLabs-Lab1-00-5.png)

   ![Paramètre de microphone](images/AzureLabs-Lab1-01.png)

> [!WARNING]
> <span data-ttu-id="7d727-153">Sachez que si vous développez pour un casque immersif pour ce laboratoire, vous risquez de rencontrer des problèmes de périphérique de sortie audio.</span><span class="sxs-lookup"><span data-stu-id="7d727-153">Be aware that if you are developing for an immersive headset for this lab, you may experience audio output device issues.</span></span> <span data-ttu-id="7d727-154">Cela est dû à un problème avec Unity, qui est résolu dans les versions ultérieures de Unity (Unity 2018,2).</span><span class="sxs-lookup"><span data-stu-id="7d727-154">This is due to an issue with Unity, which is fixed in later versions of Unity (Unity 2018.2).</span></span> <span data-ttu-id="7d727-155">Le problème empêche Unity de modifier le périphérique de sortie audio par défaut au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="7d727-155">The issue prevents Unity from changing the default audio output device at run time.</span></span> <span data-ttu-id="7d727-156">Pour contourner ce problème, assurez-vous que vous avez effectué les étapes ci-dessus et fermez et rouvrez l’éditeur, lorsque ce problème se présente lui-même.</span><span class="sxs-lookup"><span data-stu-id="7d727-156">As a work around, ensure you have completed the above steps, and close and re-open the Editor, when this issue presents itself.</span></span>

## <a name="chapter-1--the-azure-portal"></a><span data-ttu-id="7d727-157">Chapitre 1 – portail Azure</span><span class="sxs-lookup"><span data-stu-id="7d727-157">Chapter 1 – The Azure Portal</span></span>

<span data-ttu-id="7d727-158">Pour utiliser l’API Azure translator, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="7d727-158">To use the Azure Translator API, you will need to configure an instance of the Service to be made available to your application.</span></span>

1.  <span data-ttu-id="7d727-159">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d727-159">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="7d727-160">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="7d727-160">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="7d727-161">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="7d727-161">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="7d727-162">Une fois que vous êtes connecté, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez «API de traduction de texte Translator Text».</span><span class="sxs-lookup"><span data-stu-id="7d727-162">Once you are logged in, click on **New** in the top left corner and search for "Translator Text API."</span></span> <span data-ttu-id="7d727-163">Sélectionnez **entrée**.</span><span class="sxs-lookup"><span data-stu-id="7d727-163">Select **Enter**.</span></span>

    ![Nouvelle ressource](images/AzureLabs-Lab1-02.png)

    > [!NOTE]
    > <span data-ttu-id="7d727-165">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="7d727-165">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="7d727-166">La nouvelle page fournit une description du service *API de traduction de texte Translator Text* .</span><span class="sxs-lookup"><span data-stu-id="7d727-166">The new page will provide a description of the *Translator Text API* Service.</span></span> <span data-ttu-id="7d727-167">En bas à gauche de cette page, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="7d727-167">At the bottom left of this page, select the **Create** button, to create an association with this Service.</span></span>

    ![Créer un service API de traduction de texte Translator Text](images/AzureLabs-Lab1-03.png)

4.  <span data-ttu-id="7d727-169">Une fois que vous avez cliqué sur **créer**:</span><span class="sxs-lookup"><span data-stu-id="7d727-169">Once you have clicked on **Create**:</span></span>

    1. <span data-ttu-id="7d727-170">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="7d727-170">Insert your desired **Name** for this Service instance.</span></span>
    2. <span data-ttu-id="7d727-171">Sélectionnez un **abonnement**approprié.</span><span class="sxs-lookup"><span data-stu-id="7d727-171">Select an appropriate **Subscription**.</span></span>
    3. <span data-ttu-id="7d727-172">Sélectionnez le **niveau tarifaire** approprié, s’il s’agit de la première fois que vous créez un *service traduction de texte Translator Text*, vous devez disposer d’un niveau gratuit (nommé F0).</span><span class="sxs-lookup"><span data-stu-id="7d727-172">Select the **Pricing Tier** appropriate for you, if this is the first time creating a *Translator Text Service*, a free tier (named F0) should be available to you.</span></span>
    4. <span data-ttu-id="7d727-173">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="7d727-173">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="7d727-174">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="7d727-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="7d727-175">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="7d727-175">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="7d727-176">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="7d727-176">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="7d727-177">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="7d727-177">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="7d727-178">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="7d727-178">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="7d727-179">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="7d727-179">Some Azure assets are only available in certain regions.</span></span>
    6. <span data-ttu-id="7d727-180">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="7d727-180">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>
    7. <span data-ttu-id="7d727-181">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7d727-181">Select **Create**.</span></span>

        ![Sélectionnez le bouton créer.](images/AzureLabs-Lab1-04.png)

5.  <span data-ttu-id="7d727-183">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="7d727-183">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>
6.  <span data-ttu-id="7d727-184">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="7d727-184">A notification will appear in the portal once the Service instance is created.</span></span> 

    ![Notification de création de service Azure](images/AzureLabs-Lab1-05.png)

7.  <span data-ttu-id="7d727-186">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="7d727-186">Click on the notification to explore your new Service instance.</span></span> 

    ![Accédez à la fenêtre contextuelle de la ressource.](images/AzureLabs-Lab1-06.png)

8.  <span data-ttu-id="7d727-188">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="7d727-188">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> <span data-ttu-id="7d727-189">Vous êtes dirigé vers votre nouvelle instance de service API de traduction de texte Translator Text.</span><span class="sxs-lookup"><span data-stu-id="7d727-189">You will be taken to your new Translator Text API Service instance.</span></span> 

    ![Page API de traduction de texte Translator Text service](images/AzureLabs-Lab1-07.png)

9.  <span data-ttu-id="7d727-191">Dans ce didacticiel, votre application doit effectuer des appels à votre service, à l’aide de la clé d’abonnement de votre service.</span><span class="sxs-lookup"><span data-stu-id="7d727-191">Within this tutorial, your application will need to make calls to your Service, which is done through using your Service’s Subscription Key.</span></span> 
10. <span data-ttu-id="7d727-192">À partir de la page de *démarrage rapide* de votre service *traduction de texte Translator Text* , accédez à la première étape, *saisissez vos clés*, puis cliquez sur **clés** (vous pouvez également y parvenir en cliquant sur les touches de lien bleu, situées dans le menu de navigation services, indiqué par l’icône de clé).</span><span class="sxs-lookup"><span data-stu-id="7d727-192">From the *Quick start* page of your *Translator Text* Service, navigate to the first step, *Grab your keys*, and click **Keys** (you can also achieve this by clicking the blue hyperlink Keys, located in the Services navigation menu, denoted by the key icon).</span></span> <span data-ttu-id="7d727-193">Cela permet de révéler vos *clés*de service.</span><span class="sxs-lookup"><span data-stu-id="7d727-193">This will reveal your Service *Keys*.</span></span>
11. <span data-ttu-id="7d727-194">Prenez une copie de l’une des clés affichées, car vous en aurez besoin plus tard dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="7d727-194">Take a copy of one of the displayed keys, as you will need this later in your project.</span></span> 

## <a name="chapter-2--set-up-the-unity-project"></a><span data-ttu-id="7d727-195">Chapitre 2: configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="7d727-195">Chapter 2 – Set up the Unity project</span></span>

<span data-ttu-id="7d727-196">Configurez et testez votre casque immersif en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="7d727-196">Set up and test your mixed reality immersive headset.</span></span>

> [!NOTE]
> <span data-ttu-id="7d727-197">Vous n’aurez pas besoin de contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="7d727-197">You will not need motion controllers for this course.</span></span> <span data-ttu-id="7d727-198">Si vous avez besoin de la prise en charge de la configuration d’un casque immersif, [procédez comme suit](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="7d727-198">If you need support setting up an immersive headset, please [follow these steps](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

<span data-ttu-id="7d727-199">Voici une configuration standard pour le développement avec une réalité mixte et, par conséquent, est un bon modèle pour d’autres projets:</span><span class="sxs-lookup"><span data-stu-id="7d727-199">The following is a typical set up for developing with mixed reality and, as such, is a good template for other projects:</span></span>

1.  <span data-ttu-id="7d727-200">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="7d727-200">Open *Unity* and click **New**.</span></span> 

    ![Démarrez le nouveau projet Unity.](images/AzureLabs-Lab1-08.png)

2.  <span data-ttu-id="7d727-202">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-202">You will now need to provide a Unity Project name.</span></span> <span data-ttu-id="7d727-203">Insérez **MR_Translation**.</span><span class="sxs-lookup"><span data-stu-id="7d727-203">Insert **MR_Translation**.</span></span> <span data-ttu-id="7d727-204">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="7d727-204">Make sure the project type is set to **3D**.</span></span> <span data-ttu-id="7d727-205">Définissez l' *emplacement* approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="7d727-205">Set the *Location* to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="7d727-206">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="7d727-206">Then, click **Create project**.</span></span>

    ![Fournissez des détails pour le nouveau projet Unity.](images/AzureLabs-Lab1-09.png)

3.  <span data-ttu-id="7d727-208">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7d727-208">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="7d727-209">Accédez à **modifier > préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="7d727-209">Go to **Edit > Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="7d727-210">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="7d727-210">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="7d727-211">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="7d727-211">Close the **Preferences** window.</span></span>

    ![Mettre à jour la préférence éditeur de script.](images/AzureLabs-Lab1-10.png)

4.  <span data-ttu-id="7d727-213">Accédez ensuite à **fichier > paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="7d727-213">Next, go to **File > Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the **Switch Platform** button.</span></span>

    ![Fenêtre Paramètres de build, basculez plateforme vers UWP.](images/AzureLabs-Lab1-11.png)

5.  <span data-ttu-id="7d727-215">Accédez à **fichier > paramètres de build** et assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="7d727-215">Go to **File > Build Settings** and make sure that:</span></span>

    1. <span data-ttu-id="7d727-216">L' **appareil cible** est défini sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="7d727-216">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="7d727-217">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="7d727-217">For Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2. <span data-ttu-id="7d727-218">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="7d727-218">**Build Type** is set to **D3D**</span></span>
    3. <span data-ttu-id="7d727-219">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="7d727-219">**SDK** is set to **Latest installed**</span></span>
    4. <span data-ttu-id="7d727-220">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="7d727-220">**Visual Studio Version** is set to **Latest installed**</span></span>
    5. <span data-ttu-id="7d727-221">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="7d727-221">**Build and Run** is set to **Local Machine**</span></span>
    6. <span data-ttu-id="7d727-222">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="7d727-222">Save the scene and add it to the build.</span></span>

        1. <span data-ttu-id="7d727-223">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="7d727-223">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="7d727-224">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="7d727-224">A save window will appear.</span></span>

            ![Cliquez sur le bouton Ajouter des scènes ouvertes](images/AzureLabs-Lab1-12.png)

        2. <span data-ttu-id="7d727-226">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez- le Scenes.</span><span class="sxs-lookup"><span data-stu-id="7d727-226">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![Créer un dossier de scripts](images/AzureLabs-Lab1-13.png)

        3. <span data-ttu-id="7d727-228">Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier*:, tapez **MR_TranslationScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="7d727-228">Open your newly created **Scenes** folder, and then in the *File name*: text field, type **MR_TranslationScene**, then press **Save**.</span></span>

            ![Donnez un nom à la nouvelle scène.](images/AzureLabs-Lab1-14.png)

            > <span data-ttu-id="7d727-230">Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-230">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity Project.</span></span> <span data-ttu-id="7d727-231">La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-231">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>

    7. <span data-ttu-id="7d727-232">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="7d727-232">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

6. <span data-ttu-id="7d727-233">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="7d727-233">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span> 

    ![Ouvrez les paramètres du lecteur.](images/AzureLabs-Lab1-15.png)

7. <span data-ttu-id="7d727-235">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="7d727-235">In this panel, a few settings need to be verified:</span></span>

    1. <span data-ttu-id="7d727-236">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="7d727-236">In the **Other Settings** tab:</span></span>

        1. <span data-ttu-id="7d727-237">La **version du runtime de script** doit être **stable** (équivalent .net 3,5).</span><span class="sxs-lookup"><span data-stu-id="7d727-237">**Scripting Runtime Version** should be **Stable** (.NET 3.5 Equivalent).</span></span>
        2. <span data-ttu-id="7d727-238">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="7d727-238">**Scripting Backend** should be **.NET**</span></span>
        3. <span data-ttu-id="7d727-239">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="7d727-239">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Mettez à jour d’autres paramètres.](images/AzureLabs-Lab1-16.png)
      
    2. <span data-ttu-id="7d727-241">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="7d727-241">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="7d727-242">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="7d727-242">**InternetClient**</span></span>
        2. <span data-ttu-id="7d727-243">**Cravate**</span><span class="sxs-lookup"><span data-stu-id="7d727-243">**Microphone**</span></span>

            ![Mise à jour des paramètres de publication.](images/AzureLabs-Lab1-17.png)

    3. <span data-ttu-id="7d727-245">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="7d727-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![Mettez à jour les paramètres X R.](images/AzureLabs-Lab1-18.png)

8.  <span data-ttu-id="7d727-247">De retour dans les **paramètres de build**, les *projets C# Unity* ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="7d727-247">Back in **Build Settings**, *Unity C# Projects* is no longer greyed out; tick the checkbox next to this.</span></span> 
9.  <span data-ttu-id="7d727-248">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="7d727-248">Close the Build Settings window.</span></span>
10. <span data-ttu-id="7d727-249">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="7d727-249">Save your Scene and Project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-3--main-camera-setup"></a><span data-ttu-id="7d727-250">Chapitre 3 – Configuration de l’appareil photo principal</span><span class="sxs-lookup"><span data-stu-id="7d727-250">Chapter 3 – Main Camera setup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d727-251">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à [Télécharger ce fichier. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20301%20-%20Language%20translation/Azure-MR-301.unitypackage), à l’importer dans votre projet en tant que [*package personnalisé*](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [Chapitre 5](#chapter-5--create-the-results-class).</span><span class="sxs-lookup"><span data-stu-id="7d727-251">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to [download this .unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20301%20-%20Language%20translation/Azure-MR-301.unitypackage), import it into your project as a [*Custom Package*](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 5](#chapter-5--create-the-results-class).</span></span> <span data-ttu-id="7d727-252">Vous devrez toujours créer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-252">You will still need to create a Unity Project.</span></span>

1.  <span data-ttu-id="7d727-253">Dans le *volet hiérarchie*, vous trouverez un objet appelé **caméra principale**, cet objet représente le point de vue «Head» une fois que vous êtes «dans» votre application.</span><span class="sxs-lookup"><span data-stu-id="7d727-253">In the *Hierarchy Panel*, you will find an object called **Main Camera**, this object represents your “head” point of view once you are “inside” your application.</span></span>
2.  <span data-ttu-id="7d727-254">Avec le tableau de bord Unity devant vous, sélectionnez la **caméra principale gameobject**.</span><span class="sxs-lookup"><span data-stu-id="7d727-254">With the Unity Dashboard in front of you, select the **Main Camera GameObject**.</span></span> <span data-ttu-id="7d727-255">Vous remarquerez que le *panneau Inspecteur* (généralement situé à droite dans le tableau de bord) affichera les différents composants de ce *gameobject*, avec la *transformation* en haut, suivi de l' *appareil photo*et d’autres composants.</span><span class="sxs-lookup"><span data-stu-id="7d727-255">You will notice that the *Inspector Panel* (generally found to the right, within the Dashboard) will show the various components of that *GameObject*, with *Transform* at the top, followed by *Camera*, and some other components.</span></span> <span data-ttu-id="7d727-256">Vous devez réinitialiser la transformation de la caméra principale, afin qu’elle soit positionnée correctement.</span><span class="sxs-lookup"><span data-stu-id="7d727-256">You will need to reset the Transform of the Main Camera, so it is positioned correctly.</span></span>
3.  <span data-ttu-id="7d727-257">Pour ce faire, sélectionnez l’icône d' **engrenage** en regard du composant *transformer* de l’appareil photo, puis sélectionnez **Réinitialiser**.</span><span class="sxs-lookup"><span data-stu-id="7d727-257">To do this, select the **Gear** icon next to the Camera’s *Transform* component, and selecting **Reset**.</span></span> 

    ![Réinitialisez la transformation principale de l’appareil photo.](images/AzureLabs-Lab1-19.png)
 
4.  <span data-ttu-id="7d727-259">Le composant *transformer* doit alors ressembler à ceci:</span><span class="sxs-lookup"><span data-stu-id="7d727-259">The *Transform* component should then look like:</span></span>

    1. <span data-ttu-id="7d727-260">La *position* est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-260">The *Position* is set to **0, 0, 0**</span></span>
    2. <span data-ttu-id="7d727-261">La *rotation* est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-261">*Rotation* is set to **0, 0, 0**</span></span>
    3. <span data-ttu-id="7d727-262">Et *Scale* est défini sur **1, 1, 1**</span><span class="sxs-lookup"><span data-stu-id="7d727-262">And *Scale* is set to **1, 1, 1**</span></span>

        ![Informations de transformation pour l’appareil photo](images/AzureLabs-Lab1-20.png)

5.  <span data-ttu-id="7d727-264">Ensuite, avec l’objet **caméra principal** sélectionné, consultez le bouton **Ajouter un composant** situé en bas du panneau de l' *inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-264">Next, with the **Main Camera** object selected, see the **Add Component** button located at the very bottom of the *Inspector Panel*.</span></span> 
6.  <span data-ttu-id="7d727-265">Sélectionnez ce bouton et effectuez une recherche (en tapant *source audio* dans le champ de recherche ou en parcourant les sections) du composant appelé **source audio** , comme indiqué ci-dessous, puis sélectionnez-le (en appuyant sur entrée).</span><span class="sxs-lookup"><span data-stu-id="7d727-265">Select that button, and search (by either typing *Audio Source* into the search field or navigating the sections) for the component called **Audio Source** as shown below and select it (pressing enter on it also works).</span></span>
7.  <span data-ttu-id="7d727-266">Un composant *source audio* est ajouté à la **caméra principale**, comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d727-266">An *Audio Source* component will be added to the **Main Camera**, as demonstrated below.</span></span>

    ![Ajoutez un composant source audio.](images/AzureLabs-Lab1-21.png)

    > [!NOTE]
    > <span data-ttu-id="7d727-268">Pour Microsoft HoloLens, vous devrez également modifier les éléments suivants, qui font partie du composant **Camera** sur votre **caméra principale**:</span><span class="sxs-lookup"><span data-stu-id="7d727-268">For Microsoft HoloLens, you will need to also change the following, which are part of the **Camera** component on your **Main Camera**:</span></span>
    > - <span data-ttu-id="7d727-269">**Indicateurs d’effacement:** Couleur unie.</span><span class="sxs-lookup"><span data-stu-id="7d727-269">**Clear Flags:** Solid Color.</span></span>
    > - <span data-ttu-id="7d727-270">**Arrière-plan** 'Black, alpha 0 ' – couleur hexadécimale: #00000000.</span><span class="sxs-lookup"><span data-stu-id="7d727-270">**Background** ‘Black, Alpha 0’ – Hex color: #00000000.</span></span>

## <a name="chapter-4--setup-debug-canvas"></a><span data-ttu-id="7d727-271">Chapitre 4-zone de travail de débogage d’installation</span><span class="sxs-lookup"><span data-stu-id="7d727-271">Chapter 4 – Setup Debug Canvas</span></span>

<span data-ttu-id="7d727-272">Pour afficher l’entrée et la sortie de la traduction, vous devez créer une interface utilisateur de base.</span><span class="sxs-lookup"><span data-stu-id="7d727-272">To show the input and output of the translation, a basic UI needs to be created.</span></span> <span data-ttu-id="7d727-273">Pour ce cours, vous allez créer un objet d’interface utilisateur Canvas, avec plusieurs objets «Text» pour afficher les données.</span><span class="sxs-lookup"><span data-stu-id="7d727-273">For this course, you will create a Canvas UI object, with several ‘Text’ objects to show the data.</span></span>

1.  <span data-ttu-id="7d727-274">Cliquez avec le bouton droit dans une zone vide du *panneau de hiérarchie*, sous **UI**, ajoutez une zone de **dessin**.</span><span class="sxs-lookup"><span data-stu-id="7d727-274">Right-click in an empty area of the *Hierarchy Panel*, under **UI**, add a **Canvas**.</span></span>

    ![Ajoutez un nouvel objet d’interface utilisateur Canvas.](images/AzureLabs-Lab1-22.png)

2.  <span data-ttu-id="7d727-276">Lorsque l’objet canevas est sélectionné, dans le *panneau Inspecteur* (dans le composant «Canvas»), changez le **mode de rendu** en **espace universel**.</span><span class="sxs-lookup"><span data-stu-id="7d727-276">With the Canvas object selected, in the *Inspector Panel* (within the ‘Canvas’ component), change **Render Mode** to **World Space**.</span></span> 
3.  <span data-ttu-id="7d727-277">Ensuite, modifiez les paramètres suivants dans la *transformation Rect du panneau Inspecteur*:</span><span class="sxs-lookup"><span data-stu-id="7d727-277">Next, change the following parameters in the *Inspector Panel’s Rect Transform*:</span></span>

    1. <span data-ttu-id="7d727-278">*POS*    X 0 Y 0 Z 40 -  </span><span class="sxs-lookup"><span data-stu-id="7d727-278">*POS* -  **X** 0 **Y** 0 **Z** 40</span></span>
    2. <span data-ttu-id="7d727-279">*Largeur* -500</span><span class="sxs-lookup"><span data-stu-id="7d727-279">*Width* -    500</span></span>
    3. <span data-ttu-id="7d727-280">*Hauteur* -300</span><span class="sxs-lookup"><span data-stu-id="7d727-280">*Height* -   300</span></span>
    4. <span data-ttu-id="7d727-281">*Échelle*    X 0,13 Y 0,13 Z 0,13 - </span><span class="sxs-lookup"><span data-stu-id="7d727-281">*Scale* - **X** 0.13 **Y** 0.13  **Z** 0.13</span></span>

        ![Mettez à jour la transformation Rect pour la zone de dessin.](images/AzureLabs-Lab1-23.png)
 
4.  <span data-ttu-id="7d727-283">Cliquez avec le bouton droit sur le **canevas** dans le *panneau hiérarchie*, sous **interface utilisateur**, puis ajoutez un **panneau**.</span><span class="sxs-lookup"><span data-stu-id="7d727-283">Right click on the **Canvas** in the *Hierarchy Panel*, under **UI**, and add a **Panel**.</span></span> <span data-ttu-id="7d727-284">Ce **panneau** fournit un arrière-plan du texte que vous afficherez dans la scène.</span><span class="sxs-lookup"><span data-stu-id="7d727-284">This **Panel** will provide a background to the text that you will be displaying in the scene.</span></span>
5.  <span data-ttu-id="7d727-285">Cliquez avec le bouton droit sur le **panneau** dans le *volet hiérarchie*, sous **interface utilisateur**, puis ajoutez un **objet texte**.</span><span class="sxs-lookup"><span data-stu-id="7d727-285">Right click on the **Panel** in the *Hierarchy Panel*, under **UI**, and add a **Text object**.</span></span> <span data-ttu-id="7d727-286">Répétez le même processus jusqu’à ce que vous ayez créé quatre objets de texte d’interface utilisateur au total (Conseil: si le premier objet «texte» est sélectionné, vous pouvez simplement appuyer sur **«Ctrl + d»** pour le dupliquer, jusqu’à ce que vous en ayez quatre au total).</span><span class="sxs-lookup"><span data-stu-id="7d727-286">Repeat the same process until you have created four UI Text objects in total (Hint: if you have the first ‘Text’ object selected, you can simply press **‘Ctrl’ + ‘D’**, to duplicate it, until you have four in total).</span></span> 
6.  <span data-ttu-id="7d727-287">Pour chaque **objet texte**, sélectionnez-le et utilisez les tableaux ci-dessous pour définir les paramètres dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-287">For each **Text Object**, select it and use the below tables to set the parameters in the *Inspector Panel*.</span></span>

    1. <span data-ttu-id="7d727-288">Pour le composant de *transformation Rect* :</span><span class="sxs-lookup"><span data-stu-id="7d727-288">For the *Rect Transform* component:</span></span>

        | <span data-ttu-id="7d727-289">Nom</span><span class="sxs-lookup"><span data-stu-id="7d727-289">Name</span></span>                   | <span data-ttu-id="7d727-290">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="7d727-290">Transform - *Position*</span></span>             | <span data-ttu-id="7d727-291">Largeur</span><span class="sxs-lookup"><span data-stu-id="7d727-291">Width</span></span>      | <span data-ttu-id="7d727-292">Celle</span><span class="sxs-lookup"><span data-stu-id="7d727-292">Height</span></span>    |
        |:----------------------:|:----------------------------------:|:----------:|:---------:|
        | <span data-ttu-id="7d727-293">MicrophoneStatusLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-293">MicrophoneStatusLabel</span></span>  | <span data-ttu-id="7d727-294">**X** -80 **Y** 90 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-294">**X** -80 **Y** 90 **Z** 0</span></span>         | <span data-ttu-id="7d727-295">300</span><span class="sxs-lookup"><span data-stu-id="7d727-295">300</span></span>        | <span data-ttu-id="7d727-296">30</span><span class="sxs-lookup"><span data-stu-id="7d727-296">30</span></span>        |
        | <span data-ttu-id="7d727-297">AzureResponseLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-297">AzureResponseLabel</span></span>     | <span data-ttu-id="7d727-298">**X** -80 **Y** 30 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-298">**X** -80 **Y** 30 **Z** 0</span></span>         | <span data-ttu-id="7d727-299">300</span><span class="sxs-lookup"><span data-stu-id="7d727-299">300</span></span>        | <span data-ttu-id="7d727-300">30</span><span class="sxs-lookup"><span data-stu-id="7d727-300">30</span></span>        |
        | <span data-ttu-id="7d727-301">DictationLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-301">DictationLabel</span></span>         | <span data-ttu-id="7d727-302">**X** -80 **Y** -30 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-302">**X** -80 **Y** -30 **Z** 0</span></span>        | <span data-ttu-id="7d727-303">300</span><span class="sxs-lookup"><span data-stu-id="7d727-303">300</span></span>        | <span data-ttu-id="7d727-304">30</span><span class="sxs-lookup"><span data-stu-id="7d727-304">30</span></span>        |
        | <span data-ttu-id="7d727-305">TranslationResultLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-305">TranslationResultLabel</span></span> | <span data-ttu-id="7d727-306">**X** -80 **Y** -90 **Z** 0</span><span class="sxs-lookup"><span data-stu-id="7d727-306">**X** -80 **Y** -90 **Z** 0</span></span>        | <span data-ttu-id="7d727-307">300</span><span class="sxs-lookup"><span data-stu-id="7d727-307">300</span></span>        | <span data-ttu-id="7d727-308">30</span><span class="sxs-lookup"><span data-stu-id="7d727-308">30</span></span>        |


    2. <span data-ttu-id="7d727-309">Pour le composant **texte (script)** :</span><span class="sxs-lookup"><span data-stu-id="7d727-309">For the **Text (Script)** component:</span></span>


        | <span data-ttu-id="7d727-310">Nom</span><span class="sxs-lookup"><span data-stu-id="7d727-310">Name</span></span>                   | <span data-ttu-id="7d727-311">Text</span><span class="sxs-lookup"><span data-stu-id="7d727-311">Text</span></span>               | <span data-ttu-id="7d727-312">Taille de police</span><span class="sxs-lookup"><span data-stu-id="7d727-312">Font Size</span></span>    |
        |:----------------------:|:------------------:|:------------:|
        | <span data-ttu-id="7d727-313">MicrophoneStatusLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-313">MicrophoneStatusLabel</span></span>  | <span data-ttu-id="7d727-314">État du microphone:</span><span class="sxs-lookup"><span data-stu-id="7d727-314">Microphone Status:</span></span> | <span data-ttu-id="7d727-315">20</span><span class="sxs-lookup"><span data-stu-id="7d727-315">20</span></span>           |
        | <span data-ttu-id="7d727-316">AzureResponseLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-316">AzureResponseLabel</span></span>     | <span data-ttu-id="7d727-317">Réponse Web Azure</span><span class="sxs-lookup"><span data-stu-id="7d727-317">Azure Web Response</span></span> | <span data-ttu-id="7d727-318">20</span><span class="sxs-lookup"><span data-stu-id="7d727-318">20</span></span>           |
        | <span data-ttu-id="7d727-319">DictationLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-319">DictationLabel</span></span>         |   <span data-ttu-id="7d727-320">Vous avez dit:</span><span class="sxs-lookup"><span data-stu-id="7d727-320">You just said:</span></span>   | <span data-ttu-id="7d727-321">20</span><span class="sxs-lookup"><span data-stu-id="7d727-321">20</span></span>           |
        | <span data-ttu-id="7d727-322">TranslationResultLabel</span><span class="sxs-lookup"><span data-stu-id="7d727-322">TranslationResultLabel</span></span> |    <span data-ttu-id="7d727-323">Interprétation</span><span class="sxs-lookup"><span data-stu-id="7d727-323">Translation:</span></span>    | <span data-ttu-id="7d727-324">20</span><span class="sxs-lookup"><span data-stu-id="7d727-324">20</span></span>           |

        ![Entrez les valeurs correspondantes pour les étiquettes de l’interface utilisateur.](images/AzureLabs-Lab1-24.png)

    3. <span data-ttu-id="7d727-326">En outre, définissez le style de police en **gras**.</span><span class="sxs-lookup"><span data-stu-id="7d727-326">Also, make the Font Style **Bold**.</span></span> <span data-ttu-id="7d727-327">Cela rend le texte plus facile à lire.</span><span class="sxs-lookup"><span data-stu-id="7d727-327">This will make the text easier to read.</span></span>

        ![Police en gras.](images/AzureLabs-Lab1-25.png)

7.  <span data-ttu-id="7d727-329">Pour chaque *objet texte de l’interface utilisateur* créé au [Chapitre 5](#chapter-5--create-the-results-class), créez un nouvel **objet texte de l’interface utilisateur** *enfant* .</span><span class="sxs-lookup"><span data-stu-id="7d727-329">For each *UI Text object* created in [Chapter 5](#chapter-5--create-the-results-class), create a new *child* **UI Text object**.</span></span> <span data-ttu-id="7d727-330">Ces enfants affichent la sortie de l’application.</span><span class="sxs-lookup"><span data-stu-id="7d727-330">These children will display the output of the application.</span></span> <span data-ttu-id="7d727-331">Pour créer des objets *enfants* , cliquez avec le bouton droit sur le parent souhaité (par exemple, *MicrophoneStatusLabel*), puis sélectionnez **interface utilisateur** et **texte**.</span><span class="sxs-lookup"><span data-stu-id="7d727-331">Create *child* objects through right-clicking your intended parent (e.g. *MicrophoneStatusLabel*) and then select **UI** and then select **Text**.</span></span>
8.  <span data-ttu-id="7d727-332">Pour chacun de ces enfants, sélectionnez-les et utilisez les tableaux ci-dessous pour définir les paramètres dans le panneau de l’inspecteur.</span><span class="sxs-lookup"><span data-stu-id="7d727-332">For each of these children, select it and use the below tables to set the parameters in the Inspector Panel.</span></span>

    1. <span data-ttu-id="7d727-333">Pour le composant de **transformation Rect** :</span><span class="sxs-lookup"><span data-stu-id="7d727-333">For the **Rect Transform** component:</span></span>

        | <span data-ttu-id="7d727-334">Name</span><span class="sxs-lookup"><span data-stu-id="7d727-334">Name</span></span>                  | <span data-ttu-id="7d727-335">Transformation- *position*</span><span class="sxs-lookup"><span data-stu-id="7d727-335">Transform - *Position*</span></span> | <span data-ttu-id="7d727-336">Largeur</span><span class="sxs-lookup"><span data-stu-id="7d727-336">Width</span></span>      | <span data-ttu-id="7d727-337">Celle</span><span class="sxs-lookup"><span data-stu-id="7d727-337">Height</span></span>    |
        |:---------------------:|:----------------------:|:----------:|:---------:|
        | <span data-ttu-id="7d727-338">MicrophoneStatusText</span><span class="sxs-lookup"><span data-stu-id="7d727-338">MicrophoneStatusText</span></span>  | <span data-ttu-id="7d727-339">X 0 Y-30 Z 0</span><span class="sxs-lookup"><span data-stu-id="7d727-339">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="7d727-340">300</span><span class="sxs-lookup"><span data-stu-id="7d727-340">300</span></span>        | <span data-ttu-id="7d727-341">30</span><span class="sxs-lookup"><span data-stu-id="7d727-341">30</span></span>        |
        | <span data-ttu-id="7d727-342">AzureResponseText</span><span class="sxs-lookup"><span data-stu-id="7d727-342">AzureResponseText</span></span>     | <span data-ttu-id="7d727-343">X 0 Y-30 Z 0</span><span class="sxs-lookup"><span data-stu-id="7d727-343">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="7d727-344">300</span><span class="sxs-lookup"><span data-stu-id="7d727-344">300</span></span>        | <span data-ttu-id="7d727-345">30</span><span class="sxs-lookup"><span data-stu-id="7d727-345">30</span></span>        |
        | <span data-ttu-id="7d727-346">DictationText</span><span class="sxs-lookup"><span data-stu-id="7d727-346">DictationText</span></span>         | <span data-ttu-id="7d727-347">X 0 Y-30 Z 0</span><span class="sxs-lookup"><span data-stu-id="7d727-347">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="7d727-348">300</span><span class="sxs-lookup"><span data-stu-id="7d727-348">300</span></span>        | <span data-ttu-id="7d727-349">30</span><span class="sxs-lookup"><span data-stu-id="7d727-349">30</span></span>        |
        | <span data-ttu-id="7d727-350">TranslationResultText</span><span class="sxs-lookup"><span data-stu-id="7d727-350">TranslationResultText</span></span> | <span data-ttu-id="7d727-351">X 0 Y-30 Z 0</span><span class="sxs-lookup"><span data-stu-id="7d727-351">X 0 Y -30 Z 0</span></span>          | <span data-ttu-id="7d727-352">300</span><span class="sxs-lookup"><span data-stu-id="7d727-352">300</span></span>        | <span data-ttu-id="7d727-353">30</span><span class="sxs-lookup"><span data-stu-id="7d727-353">30</span></span>        |

    2. <span data-ttu-id="7d727-354">Pour le composant **texte (script)** :</span><span class="sxs-lookup"><span data-stu-id="7d727-354">For the **Text (Script)** component:</span></span>

        | <span data-ttu-id="7d727-355">Name</span><span class="sxs-lookup"><span data-stu-id="7d727-355">Name</span></span>                  | <span data-ttu-id="7d727-356">Text</span><span class="sxs-lookup"><span data-stu-id="7d727-356">Text</span></span>          | <span data-ttu-id="7d727-357">Taille de police</span><span class="sxs-lookup"><span data-stu-id="7d727-357">Font Size</span></span>    |
        |:---------------------:|:-------------:|:------------:|
        | <span data-ttu-id="7d727-358">MicrophoneStatusText</span><span class="sxs-lookup"><span data-stu-id="7d727-358">MicrophoneStatusText</span></span>  |      <span data-ttu-id="7d727-359">??</span><span class="sxs-lookup"><span data-stu-id="7d727-359">??</span></span>       | <span data-ttu-id="7d727-360">20</span><span class="sxs-lookup"><span data-stu-id="7d727-360">20</span></span>           |
        | <span data-ttu-id="7d727-361">AzureResponseText</span><span class="sxs-lookup"><span data-stu-id="7d727-361">AzureResponseText</span></span>     |      <span data-ttu-id="7d727-362">??</span><span class="sxs-lookup"><span data-stu-id="7d727-362">??</span></span>       | <span data-ttu-id="7d727-363">20</span><span class="sxs-lookup"><span data-stu-id="7d727-363">20</span></span>           |
        | <span data-ttu-id="7d727-364">DictationText</span><span class="sxs-lookup"><span data-stu-id="7d727-364">DictationText</span></span>         |      <span data-ttu-id="7d727-365">??</span><span class="sxs-lookup"><span data-stu-id="7d727-365">??</span></span>       | <span data-ttu-id="7d727-366">20</span><span class="sxs-lookup"><span data-stu-id="7d727-366">20</span></span>           |
        | <span data-ttu-id="7d727-367">TranslationResultText</span><span class="sxs-lookup"><span data-stu-id="7d727-367">TranslationResultText</span></span> |      <span data-ttu-id="7d727-368">??</span><span class="sxs-lookup"><span data-stu-id="7d727-368">??</span></span>       | <span data-ttu-id="7d727-369">20</span><span class="sxs-lookup"><span data-stu-id="7d727-369">20</span></span>           |

9. <span data-ttu-id="7d727-370">Ensuite, sélectionnez l’option d’alignement «Centre» pour chaque composant de texte:</span><span class="sxs-lookup"><span data-stu-id="7d727-370">Next, select the 'centre' alignment option for each text component:</span></span>

    ![aligner le texte.](images/AzureLabs-Lab1-26.png)

10. <span data-ttu-id="7d727-372">Pour vous assurer que les objets texte de l' **interface utilisateur enfant** sont facilement lisibles, modifiez leur *couleur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-372">To ensure the **child UI Text** objects are easily readable, change their *Color*.</span></span> <span data-ttu-id="7d727-373">Pour ce faire, cliquez sur la barre («noire» actuellement) en regard de la *couleur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-373">Do this by clicking on the bar (currently ‘Black’) next to *Color*.</span></span> 

    ![Entrez les valeurs correspondantes pour les sorties de texte de l’interface utilisateur.](images/AzureLabs-Lab1-27.png)
 
11. <span data-ttu-id="7d727-375">Ensuite, dans la fenêtre nouvelle *couleur* , modifiez la *couleur hexadécimale* en: **0032EAFF**</span><span class="sxs-lookup"><span data-stu-id="7d727-375">Then, in the new, little, *Color* window, change the *Hex Color* to: **0032EAFF**</span></span>

    ![Mettez à jour la couleur en bleu.](images/AzureLabs-Lab1-28.png)
 
12. <span data-ttu-id="7d727-377">Vous trouverez ci-dessous l’aspect de l' **interface utilisateur** .</span><span class="sxs-lookup"><span data-stu-id="7d727-377">Below is how the **UI** should look.</span></span>
    1.  <span data-ttu-id="7d727-378">Dans le *volet hiérarchie*:</span><span class="sxs-lookup"><span data-stu-id="7d727-378">In the *Hierarchy Panel*:</span></span>

        ![Avoir une hiérarchie dans la structure fournie.](images/AzureLabs-Lab1-29.png)

    2.  <span data-ttu-id="7d727-380">Dans les vues *scène* et *jeu*:</span><span class="sxs-lookup"><span data-stu-id="7d727-380">In the *Scene* and *Game Views*:</span></span>

        ![Avoir les vues scène et jeu dans la même structure.](images/AzureLabs-Lab1-30.png)

## <a name="chapter-5--create-the-results-class"></a><span data-ttu-id="7d727-382">Chapitre 5: créer la classe Results</span><span class="sxs-lookup"><span data-stu-id="7d727-382">Chapter 5 – Create the Results class</span></span>

<span data-ttu-id="7d727-383">Le premier script que vous devez créer est la  classe Results, qui est chargée de fournir un moyen de voir les résultats de la traduction.</span><span class="sxs-lookup"><span data-stu-id="7d727-383">The first script you need to create is the *Results* class, which is responsible for providing a way to see the results of translation.</span></span> <span data-ttu-id="7d727-384">La classe stocke et affiche les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="7d727-384">The Class stores and displays the following:</span></span> 

- <span data-ttu-id="7d727-385">Résultat de la réponse d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7d727-385">The response result from Azure.</span></span>
- <span data-ttu-id="7d727-386">État du microphone.</span><span class="sxs-lookup"><span data-stu-id="7d727-386">The microphone status.</span></span> 
- <span data-ttu-id="7d727-387">Résultat de la dictée (voix au texte).</span><span class="sxs-lookup"><span data-stu-id="7d727-387">The result of the dictation (voice to text).</span></span>
- <span data-ttu-id="7d727-388">Résultat de la traduction.</span><span class="sxs-lookup"><span data-stu-id="7d727-388">The result of the translation.</span></span>

<span data-ttu-id="7d727-389">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="7d727-389">To create this class:</span></span> 

1.  <span data-ttu-id="7d727-390">Cliquez avec le bouton droit dans le *panneau Projet*, puis **créez > dossier**.</span><span class="sxs-lookup"><span data-stu-id="7d727-390">Right-click in the *Project Panel*, then **Create > Folder**.</span></span> <span data-ttu-id="7d727-391">Nommez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="7d727-391">Name the folder **Scripts**.</span></span> 
 
    ![Créer un dossier de scripts.](images/AzureLabs-Lab1-31.png)

    ![Ouvrez le dossier scripts.](images/AzureLabs-Lab1-32.png)
 
2.  <span data-ttu-id="7d727-394">Avec le dossier **scripts** créer, double-cliquez dessus pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="7d727-394">With the **Scripts** folder create, double click it to open.</span></span> <span data-ttu-id="7d727-395">Ensuite, dans ce dossier, cliquez avec le bouton droit, puis sélectionnez **créer >**  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="7d727-395">Then within that folder, right-click, and select **Create >** then **C# Script**.</span></span> <span data-ttu-id="7d727-396">Nommez les *résultats*du script.</span><span class="sxs-lookup"><span data-stu-id="7d727-396">Name the script *Results*.</span></span> 

    ![Créez le premier script.](images/AzureLabs-Lab1-33.png)
 
3.  <span data-ttu-id="7d727-398">Double-cliquez sur le  nouveau script Results pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7d727-398">Double click on the new *Results* script to open it with **Visual Studio**.</span></span>
4.  <span data-ttu-id="7d727-399">Insérez les espaces de noms suivants:</span><span class="sxs-lookup"><span data-stu-id="7d727-399">Insert the following namespaces:</span></span>

    ```cs
        using UnityEngine;
        using UnityEngine.UI;
    ```

5.  <span data-ttu-id="7d727-400">À l’intérieur de la classe, insérez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d727-400">Inside the Class insert the following variables:</span></span>

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

6.  <span data-ttu-id="7d727-401">Ajoutez ensuite la méthode *éveillé ()* , qui sera appelée lors de l’initialisation de la classe.</span><span class="sxs-lookup"><span data-stu-id="7d727-401">Then add the *Awake()* method, which will be called when the class initializes.</span></span> 

    ```csharp
        private void Awake() 
        { 
            // Set this class to behave similar to singleton 
            instance = this;           
        } 
    ```

7.  <span data-ttu-id="7d727-402">Enfin, ajoutez les méthodes qui sont chargées de sortir les différentes informations de résultats à l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7d727-402">Finally, add the methods which are responsible for outputting the various results information to the UI.</span></span> 

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

8.  <span data-ttu-id="7d727-403">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-403">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-6--create-the-microphonemanager-class"></a><span data-ttu-id="7d727-404">Chapitre 6: créer la classe *MicrophoneManager*</span><span class="sxs-lookup"><span data-stu-id="7d727-404">Chapter 6 – Create the *MicrophoneManager* class</span></span>

<span data-ttu-id="7d727-405">La deuxième classe que vous allez créer est *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="7d727-405">The second class you are going to create is the *MicrophoneManager*.</span></span>

<span data-ttu-id="7d727-406">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d727-406">This class is responsible for:</span></span>

- <span data-ttu-id="7d727-407">Détection du périphérique d’enregistrement attaché au casque ou à l’ordinateur (selon la valeur par défaut).</span><span class="sxs-lookup"><span data-stu-id="7d727-407">Detecting the recording device attached to the headset or machine (whichever is the default).</span></span>
- <span data-ttu-id="7d727-408">Capturez l’audio (voix) et utilisez la dictée pour le stocker en tant que chaîne.</span><span class="sxs-lookup"><span data-stu-id="7d727-408">Capture the audio (voice) and use dictation to store it as a string.</span></span>
- <span data-ttu-id="7d727-409">Une fois que la voix a été suspendue, soumettez la dictée à la classe translator.</span><span class="sxs-lookup"><span data-stu-id="7d727-409">Once the voice has paused, submit the dictation to the Translator class.</span></span>
- <span data-ttu-id="7d727-410">Hébergez une méthode qui peut arrêter la capture de la voix si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="7d727-410">Host a method that can stop the voice capture if desired.</span></span>

<span data-ttu-id="7d727-411">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="7d727-411">To create this class:</span></span> 
1.  <span data-ttu-id="7d727-412">Double-cliquez sur le dossier **scripts** pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="7d727-412">Double click on the **Scripts** folder, to open it.</span></span> 
2.  <span data-ttu-id="7d727-413">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer > C# script**.</span><span class="sxs-lookup"><span data-stu-id="7d727-413">Right-click inside the **Scripts** folder, click **Create > C# Script**.</span></span> <span data-ttu-id="7d727-414">Nommez le script *MicrophoneManager*.</span><span class="sxs-lookup"><span data-stu-id="7d727-414">Name the script *MicrophoneManager*.</span></span> 
3.  <span data-ttu-id="7d727-415">Double-cliquez sur le nouveau script pour l’ouvrir avec Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7d727-415">Double click on the new script to open it with Visual Studio.</span></span>
4.  <span data-ttu-id="7d727-416">Mettez à jour les espaces de noms pour qu’ils soient identiques à ce qui suit, en haut de la classe *MicrophoneManager* :</span><span class="sxs-lookup"><span data-stu-id="7d727-416">Update the namespaces to be the same as the following, at the top of the *MicrophoneManager* class:</span></span>

    ```csharp
        using UnityEngine; 
        using UnityEngine.Windows.Speech;
    ```

5.  <span data-ttu-id="7d727-417">Ensuite, ajoutez les variables suivantes à l’intérieur de la classe *MicrophoneManager* :</span><span class="sxs-lookup"><span data-stu-id="7d727-417">Then, add the following variables inside the *MicrophoneManager* class:</span></span>

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

6.  <span data-ttu-id="7d727-418">Vous devez maintenant ajouter du code pour les méthodes *éveillé ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="7d727-418">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span> <span data-ttu-id="7d727-419">Ils sont appelés lorsque la classe est initialisée:</span><span class="sxs-lookup"><span data-stu-id="7d727-419">These will be called when the class initializes:</span></span>

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

7.  <span data-ttu-id="7d727-420">Vous pouvez *supprimer* la méthode *Update ()* puisque cette classe ne l’utilise pas.</span><span class="sxs-lookup"><span data-stu-id="7d727-420">You can *delete* the *Update()* method since this class will not use it.</span></span>
8.  <span data-ttu-id="7d727-421">À présent, vous avez besoin des méthodes que l’application utilise pour démarrer et arrêter la capture vocale, et la passer à la classe *Translator* , que vous allez bientôt créer.</span><span class="sxs-lookup"><span data-stu-id="7d727-421">Now you need the methods that the App uses to start and stop the voice capture, and pass it to the *Translator* class, that you will build soon.</span></span> <span data-ttu-id="7d727-422">Copiez le code suivant et collez-le sous la méthode *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="7d727-422">Copy the following code and paste it beneath the *Start()* method.</span></span>

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
    > <span data-ttu-id="7d727-423">Bien que cette application ne l’utilise pas, la méthode *StopCapturingAudio ()* a également été fournie ici, si vous souhaitez implémenter la possibilité d’arrêter la capture de l’audio dans votre application.</span><span class="sxs-lookup"><span data-stu-id="7d727-423">Though this application will not make use of it, the *StopCapturingAudio()* method has also been provided here, should you want to implement the ability to stop capturing audio in your application.</span></span>

9.  <span data-ttu-id="7d727-424">Vous devez maintenant ajouter un gestionnaire de dictée qui sera appelé lorsque la voix s’arrêtera.</span><span class="sxs-lookup"><span data-stu-id="7d727-424">You now need to add a Dictation Handler that will be invoked when the voice stops.</span></span> <span data-ttu-id="7d727-425">Cette méthode passera ensuite le texte dicté à la classe *Translator* .</span><span class="sxs-lookup"><span data-stu-id="7d727-425">This method will then pass the dictated text to the *Translator* class.</span></span>

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

10. <span data-ttu-id="7d727-426">Veillez à enregistrer vos modifications dans Visual Studio avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-426">Be sure to save your changes in Visual Studio before returning to Unity.</span></span>

> [!WARNING]  
> <span data-ttu-id="7d727-427">À ce stade, vous remarquerez qu’une erreur s’affiche dans le panneau de la console de l' *éditeur Unity* («le nom’Translator’n’existe pas...»).</span><span class="sxs-lookup"><span data-stu-id="7d727-427">At this point you will notice an error appearing in the *Unity Editor Console* Panel (“The name ‘Translator’ does not exist...”).</span></span> <span data-ttu-id="7d727-428">Cela est dû au fait que le code fait référence à la classe *Translator* , que vous allez créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="7d727-428">This is because the code references the *Translator* class, which you will create in the next chapter.</span></span>

## <a name="chapter-7--call-to-azure-and-translator-service"></a><span data-ttu-id="7d727-429">Chapitre 7 – appel à Azure et au service de traduction</span><span class="sxs-lookup"><span data-stu-id="7d727-429">Chapter 7 – Call to Azure and translator service</span></span>

<span data-ttu-id="7d727-430">Le dernier script que vous devez créer est la classe *Translator* .</span><span class="sxs-lookup"><span data-stu-id="7d727-430">The last script you need to create is the *Translator* class.</span></span> 

<span data-ttu-id="7d727-431">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d727-431">This class is responsible for:</span></span>

-   <span data-ttu-id="7d727-432">Authentification de l’application avec *Azure*, en échange d’un **jeton d’authentification**.</span><span class="sxs-lookup"><span data-stu-id="7d727-432">Authenticating the App with *Azure*, in exchange for an **Auth Token**.</span></span>
-   <span data-ttu-id="7d727-433">Utilisez le **jeton d’authentification** pour envoyer du texte (reçu à partir de la classe *MicrophoneManager* ) à traduire.</span><span class="sxs-lookup"><span data-stu-id="7d727-433">Use the **Auth Token** to submit text (received from the *MicrophoneManager* Class) to be translated.</span></span>
-   <span data-ttu-id="7d727-434">Recevoir le résultat traduit et le passer à la  classe Results pour le visualiser dans l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7d727-434">Receive the translated result and pass it to the *Results* Class to be visualized in the UI.</span></span>

<span data-ttu-id="7d727-435">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="7d727-435">To create this Class:</span></span> 
1.  <span data-ttu-id="7d727-436">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="7d727-436">Go to the **Scripts** folder you created previously.</span></span> 
2.  <span data-ttu-id="7d727-437">Cliquez avec le bouton droit dans le **panneau Projet**, puis **créez > C# script**.</span><span class="sxs-lookup"><span data-stu-id="7d727-437">Right-click in the **Project Panel**, **Create > C# Script**.</span></span> <span data-ttu-id="7d727-438">Appelez le *traducteur*de script.</span><span class="sxs-lookup"><span data-stu-id="7d727-438">Call the script *Translator*.</span></span>
3.  <span data-ttu-id="7d727-439">Double-cliquez sur le script du nouveau *convertisseur* pour l’ouvrir **avec Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="7d727-439">Double click on the new *Translator* script to open it **with Visual Studio**.</span></span>
4.  <span data-ttu-id="7d727-440">Ajoutez les espaces de noms suivants au début du fichier:</span><span class="sxs-lookup"><span data-stu-id="7d727-440">Add the following namespaces to the top of the file:</span></span>

    ```csharp
        using System;
        using System.Collections;
        using System.Xml.Linq;
        using UnityEngine;
        using UnityEngine.Networking;
    ```

5.  <span data-ttu-id="7d727-441">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *Translator* :</span><span class="sxs-lookup"><span data-stu-id="7d727-441">Then add the following variables inside the *Translator* class:</span></span>

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
    > - <span data-ttu-id="7d727-442">Les langages insérés dans  l’énumération Languages sont simplement des exemples.</span><span class="sxs-lookup"><span data-stu-id="7d727-442">The languages inserted into the languages **enum** are just examples.</span></span> <span data-ttu-id="7d727-443">N’hésitez pas à en ajouter d’autres si vous le souhaitez. l' [API prend en charge plus de 60 langues](https://docs.microsoft.com/azure/cognitive-services/translator/languages) (y compris Klingon)!</span><span class="sxs-lookup"><span data-stu-id="7d727-443">Feel free to add more if you wish; the [API supports over 60 languages](https://docs.microsoft.com/azure/cognitive-services/translator/languages) (including Klingon)!</span></span>
    > - <span data-ttu-id="7d727-444">Il existe une [page plus interactive couvrant les langues disponibles](https://www.microsoft.com/translator/business/languages/). Toutefois, sachez que la page semble fonctionner uniquement lorsque la langue du site est définie sur «en-US» (et que le site Microsoft est susceptible de rediriger vers votre langue native).</span><span class="sxs-lookup"><span data-stu-id="7d727-444">There is a [more interactive page covering available languages](https://www.microsoft.com/translator/business/languages/), though be aware the page only appears to work when the site language is set to 'en-us' (and the Microsoft site will likely redirect to your native language).</span></span> <span data-ttu-id="7d727-445">Vous pouvez modifier la langue du site en bas de la page ou en modifiant l’URL.</span><span class="sxs-lookup"><span data-stu-id="7d727-445">You can change site language at the bottom of the page or by altering the URL.</span></span>
    > - <span data-ttu-id="7d727-446">La valeur **authorizationKey** , dans l’extrait de code ci-dessus, doit être la **clé** que vous avez reçue lorsque vous vous êtes abonné au *API de traduction de texte Translator Text Azure*.</span><span class="sxs-lookup"><span data-stu-id="7d727-446">The **authorizationKey** value, in the above code snippet, must be the **Key**  you received when you subscribed to the *Azure Translator Text API*.</span></span> <span data-ttu-id="7d727-447">Ce sujet a été abordé dans le [Chapitre 1](#chapter-1--the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="7d727-447">This was covered in [Chapter 1](#chapter-1--the-azure-portal).</span></span>

6.  <span data-ttu-id="7d727-448">Vous devez maintenant ajouter du code pour les méthodes *éveillé ()* et *Start ()* .</span><span class="sxs-lookup"><span data-stu-id="7d727-448">Code for the *Awake()* and *Start()* methods now needs to be added.</span></span> 
7.  <span data-ttu-id="7d727-449">Dans ce cas, le code fait un appel à *Azure* à l’aide de la clé d’autorisation pour obtenir un *jeton*.</span><span class="sxs-lookup"><span data-stu-id="7d727-449">In this case, the code will make a call to *Azure* using the authorization Key, to get a *Token*.</span></span>

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
    > <span data-ttu-id="7d727-450">Le jeton expire au bout de 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7d727-450">The token will expire after 10 minutes.</span></span> <span data-ttu-id="7d727-451">Selon le scénario de votre application, vous devrez peut-être effectuer plusieurs fois le même appel de Coroutine.</span><span class="sxs-lookup"><span data-stu-id="7d727-451">Depending on the scenario for your app, you might have to make the same coroutine call multiple times.</span></span>

8.  <span data-ttu-id="7d727-452">La Coroutine permettant d’obtenir le jeton est la suivante:</span><span class="sxs-lookup"><span data-stu-id="7d727-452">The coroutine to obtain the Token is the following:</span></span>

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
    > <span data-ttu-id="7d727-453">Si vous modifiez le nom de la méthode IEnumerator **GetTokenCoroutine ()** , vous devez mettre à jour les valeurs de chaîne d’appel *StartCoroutine* et *StopCoroutine* dans le code ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="7d727-453">If you edit the name of the IEnumerator method **GetTokenCoroutine()**, you need to update the *StartCoroutine* and *StopCoroutine* call string values in the above code.</span></span> <span data-ttu-id="7d727-454">[En](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StartCoroutine.html)fonction de la documentation Unity, pour arrêter une Coroutine spécifique, vous devez utiliser la méthode de valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="7d727-454">[As per Unity documentation](https://docs.unity3d.com/ScriptReference/MonoBehaviour.StartCoroutine.html), to Stop a specific *Coroutine*, you need to use the string value method.</span></span>

9.  <span data-ttu-id="7d727-455">Ensuite, ajoutez la Coroutine (avec une méthode de flux «support» juste en dessous) pour obtenir la traduction du texte reçu par la classe *MicrophoneManager* .</span><span class="sxs-lookup"><span data-stu-id="7d727-455">Next, add the coroutine (with a “support” stream method right below it) to obtain the translation of the text received by the *MicrophoneManager* class.</span></span> <span data-ttu-id="7d727-456">Ce code crée une chaîne de requête à envoyer à l' *API de traduction de texte Translator Text Azure*, puis utilise la classe UnityWebRequest Unity interne pour effectuer un appel’obtenir’au point de terminaison avec la chaîne de requête.</span><span class="sxs-lookup"><span data-stu-id="7d727-456">This code creates a query string to send to the *Azure Translator Text API*, and then uses the internal Unity UnityWebRequest class to make a ‘Get’ call to the endpoint with the query string.</span></span> <span data-ttu-id="7d727-457">Le résultat est ensuite utilisé pour définir la traduction dans votre objet de résultats.</span><span class="sxs-lookup"><span data-stu-id="7d727-457">The result is then used to set the translation in your Results object.</span></span> <span data-ttu-id="7d727-458">Le code ci-dessous illustre l’implémentation:</span><span class="sxs-lookup"><span data-stu-id="7d727-458">The code below shows the implementation:</span></span>

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

10. <span data-ttu-id="7d727-459">Veillez à enregistrer vos modifications dans *Visual Studio* avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-459">Be sure to save your changes in *Visual Studio* before returning to *Unity*.</span></span>

## <a name="chapter-8--configure-the-unity-scene"></a><span data-ttu-id="7d727-460">Chapitre 8 – configurer la scène Unity</span><span class="sxs-lookup"><span data-stu-id="7d727-460">Chapter 8 – Configure the Unity Scene</span></span>

1.  <span data-ttu-id="7d727-461">De retour dans l’éditeur Unity, cliquez et  faites glisser la classe Results *du* dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="7d727-461">Back in the Unity Editor, click and drag the *Results* class *from* the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>
2.  <span data-ttu-id="7d727-462">Cliquez sur l' **appareil photo principal** et observez le panneau de l' *inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-462">Click on the **Main Camera** and look at the *Inspector Panel*.</span></span> <span data-ttu-id="7d727-463">Vous remarquerez que dans le composant *script* nouvellement ajouté, il y a quatre champs avec des valeurs vides.</span><span class="sxs-lookup"><span data-stu-id="7d727-463">You will notice that within the newly added *Script* component, there are four fields with empty values.</span></span> <span data-ttu-id="7d727-464">Il s’agit des références de sortie des propriétés dans le code.</span><span class="sxs-lookup"><span data-stu-id="7d727-464">These are the output references to the properties in the code.</span></span> 
3.  <span data-ttu-id="7d727-465">Faites glisser les objets de **texte** appropriés du volet de la *hiérarchie* vers ces quatre emplacements, comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="7d727-465">Drag the appropriate **Text** objects from the *Hierarchy Panel* to those four slots, as shown in the image below.</span></span>

    ![Met à jour les références cibles avec les valeurs spécifiées.](images/AzureLabs-Lab1-34.png)
  
4.  <span data-ttu-id="7d727-467">Ensuite, cliquez et faites glisser la classe *Translator* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="7d727-467">Next, click and drag the *Translator* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 
5.  <span data-ttu-id="7d727-468">Ensuite, cliquez et faites glisser la classe *MicrophoneManager* du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="7d727-468">Then, click and drag the *MicrophoneManager* class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span> 
6.  <span data-ttu-id="7d727-469">Enfin, cliquez sur l' **appareil photo principal** et observez le panneau de l' *inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="7d727-469">Lastly, click on the **Main Camera** and look at the *Inspector Panel*.</span></span> <span data-ttu-id="7d727-470">Vous remarquerez que dans le script que vous avez glissé, il existe deux zones de liste déroulante qui vous permettent de définir les langues.</span><span class="sxs-lookup"><span data-stu-id="7d727-470">You will notice that in the script you dragged on, there are two drop down boxes that will allow you to set the languages.</span></span>
 
    ![Vérifiez que les langues de traduction prévues sont entrées.](images/AzureLabs-Lab1-35.png)

## <a name="chapter-9--test-in-mixed-reality"></a><span data-ttu-id="7d727-472">Chapitre 9 – test en réalité mixte</span><span class="sxs-lookup"><span data-stu-id="7d727-472">Chapter 9 – Test in mixed reality</span></span>

<span data-ttu-id="7d727-473">À ce stade, vous devez vérifier que la scène a été correctement implémentée.</span><span class="sxs-lookup"><span data-stu-id="7d727-473">At this point you need to test that the Scene has been properly implemented.</span></span>

<span data-ttu-id="7d727-474">Assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="7d727-474">Ensure that:</span></span>

- <span data-ttu-id="7d727-475">Tous les paramètres mentionnés dans le [Chapitre 1](#chapter-1--the-azure-portal) sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="7d727-475">All the settings mentioned in [Chapter 1](#chapter-1--the-azure-portal) are set correctly.</span></span> 
- <span data-ttu-id="7d727-476">Les *résultats*, *Translator*et *MicrophoneManager*, les scripts sont attachés à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="7d727-476">The *Results*, *Translator*, and *MicrophoneManager*, scripts are attached to the **Main Camera** object.</span></span> 
- <span data-ttu-id="7d727-477">Vous avez placé votre **clé** de Service *Azure API de traduction de texte Translator Text* dans la variable **AuthorizationKey** dans le script du *traducteur* .</span><span class="sxs-lookup"><span data-stu-id="7d727-477">You have placed your *Azure Translator Text API* Service **Key** within the **authorizationKey** variable within the *Translator* Script.</span></span>  
- <span data-ttu-id="7d727-478">Tous les champs du volet principal de l’inspecteur de l' *appareil photo* sont correctement affectés.</span><span class="sxs-lookup"><span data-stu-id="7d727-478">All the fields in the *Main Camera Inspector Panel* are assigned properly.</span></span>
- <span data-ttu-id="7d727-479">Votre microphone fonctionne lors de l’exécution de votre scène (dans le cas contraire, vérifiez que votre microphone attaché est l’appareil *par défaut* et que vous l’avez [configuré correctement dans Windows](https://support.microsoft.com/en-au/help/4027981/windows-how-to-set-up-and-test-microphones-in-windows-10)).</span><span class="sxs-lookup"><span data-stu-id="7d727-479">Your microphone is working when running your scene (if not, check that your attached microphone is the *default* device, and that you have [set it up correctly within Windows](https://support.microsoft.com/en-au/help/4027981/windows-how-to-set-up-and-test-microphones-in-windows-10)).</span></span>

<span data-ttu-id="7d727-480">Vous pouvez tester le casque immersif en appuyant sur le bouton **lecture** dans l' *éditeur Unity*.</span><span class="sxs-lookup"><span data-stu-id="7d727-480">You can test the immersive headset by pressing the **Play** button in the *Unity Editor*.</span></span>
<span data-ttu-id="7d727-481">L’application doit fonctionner par le biais du casque immersif attaché.</span><span class="sxs-lookup"><span data-stu-id="7d727-481">The App should be functioning through the attached immersive headset.</span></span>

> [!WARNING]  
> <span data-ttu-id="7d727-482">Si une erreur s’affiche dans la console Unity à propos du changement de périphérique audio par défaut, la scène peut ne pas fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="7d727-482">If you see an error in the Unity console about the default audio device changing, the scene may not function as expected.</span></span> <span data-ttu-id="7d727-483">Cela est dû à la façon dont le portail de réalité mixte traite les microphones intégrés pour les casques.</span><span class="sxs-lookup"><span data-stu-id="7d727-483">This is due to the way the mixed reality portal deals with built-in microphones for headsets that have them.</span></span> <span data-ttu-id="7d727-484">Si vous voyez cette erreur, arrêtez simplement la scène et redémarrez-la et les choses devraient fonctionner comme prévu.</span><span class="sxs-lookup"><span data-stu-id="7d727-484">If you see this error, simply stop the scene and start it again and things should work as expected.</span></span>

## <a name="chapter-10--build-the-uwp-solution-and-sideload-on-local-machine"></a><span data-ttu-id="7d727-485">Chapitre 10: créer la solution UWP et chargement sur l’ordinateur local</span><span class="sxs-lookup"><span data-stu-id="7d727-485">Chapter 10 – Build the UWP solution and sideload on local machine</span></span>

<span data-ttu-id="7d727-486">Tout ce qui est nécessaire pour la section Unity de ce projet est maintenant terminé. il est donc temps de la générer à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="7d727-486">Everything needed for the Unity section of this project has now been completed, so it is time to build it from Unity.</span></span>

1.  <span data-ttu-id="7d727-487">Accédez à **paramètres de build**: **Paramètres de build du fichier >...**</span><span class="sxs-lookup"><span data-stu-id="7d727-487">Navigate to **Build Settings**: **File > Build Settings...**</span></span>
2.  <span data-ttu-id="7d727-488">Dans la fenêtre **paramètres de build** , cliquez sur **générer**.</span><span class="sxs-lookup"><span data-stu-id="7d727-488">From the **Build Settings** window, click **Build**.</span></span>

    ![Générez la scène Unity.](images/AzureLabs-Lab1-36.png)
  
3.  <span data-ttu-id="7d727-490">Si ce n’est pas déjà fait, les **projets C# Unity**.</span><span class="sxs-lookup"><span data-stu-id="7d727-490">If not already, tick **Unity C# Projects**.</span></span>
4.  <span data-ttu-id="7d727-491">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="7d727-491">Click **Build**.</span></span> <span data-ttu-id="7d727-492">Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="7d727-492">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="7d727-493">Créez ce dossier maintenant, puis nommez-le *application*.</span><span class="sxs-lookup"><span data-stu-id="7d727-493">Create that folder now, and name it *App*.</span></span> <span data-ttu-id="7d727-494">Ensuite, avec le dossier d' *application* sélectionné, appuyez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="7d727-494">Then with the *App* folder selected, press **Select Folder**.</span></span> 
5.  <span data-ttu-id="7d727-495">Unity commence à générer votre projet dans le dossier de l' *application* .</span><span class="sxs-lookup"><span data-stu-id="7d727-495">Unity will begin building your project to the *App* folder.</span></span> 
6.  <span data-ttu-id="7d727-496">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' *Explorateur de fichiers* s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="7d727-496">Once Unity has finished building (it might take some time), it will open a *File Explorer* window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-11--deploy-your-application"></a><span data-ttu-id="7d727-497">Chapitre 11 – déployer votre application</span><span class="sxs-lookup"><span data-stu-id="7d727-497">Chapter 11 – Deploy your application</span></span>

<span data-ttu-id="7d727-498">Pour déployer votre application:</span><span class="sxs-lookup"><span data-stu-id="7d727-498">To deploy your application:</span></span>

1.  <span data-ttu-id="7d727-499">Accédez à votre nouvelle build Unity (le dossier de l' *application* ) et ouvrez le fichier solution avec *Visual Studio*.</span><span class="sxs-lookup"><span data-stu-id="7d727-499">Navigate to your new Unity build (the *App* folder) and open the solution file with *Visual Studio*.</span></span>
2.  <span data-ttu-id="7d727-500">Dans la configuration de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="7d727-500">In the Solution Configuration select **Debug**.</span></span>
3.  <span data-ttu-id="7d727-501">Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="7d727-501">In the Solution Platform, select **x86**, **Local Machine**.</span></span> 

    > <span data-ttu-id="7d727-502">Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine*distante, afin de ne pas être attaché à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="7d727-502">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="7d727-503">Toutefois, vous devez également effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="7d727-503">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="7d727-504">Identifiez l' **adresse IP** de votre HoloLens, qui se trouve dans les *paramètres > réseau & Internet > les options avancées du Wi-Fi >* ; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="7d727-504">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="7d727-505">Assurez-vous que le *mode développeur* est **activé**; trouvé dans *paramètres > mettre à jour & > de sécurité pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="7d727-505">Ensure *Developer Mode* is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Déployez la solution à partir de Visual Studio.](images/AzureLabs-Lab1-37.png)
    
 
4.  <span data-ttu-id="7d727-507">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="7d727-507">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your PC.</span></span>
5.  <span data-ttu-id="7d727-508">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="7d727-508">Your App should now appear in the list of installed apps, ready to be launched.</span></span>
6.  <span data-ttu-id="7d727-509">Une fois lancé, l’application vous invite à autoriser l’accès au microphone.</span><span class="sxs-lookup"><span data-stu-id="7d727-509">Once launched, the App will prompt you to authorize access to the Microphone.</span></span> <span data-ttu-id="7d727-510">Veillez à cliquer sur le bouton **Oui** .</span><span class="sxs-lookup"><span data-stu-id="7d727-510">Make sure to click the **YES** button.</span></span>
7.  <span data-ttu-id="7d727-511">Vous êtes maintenant prêt à commencer la traduction.</span><span class="sxs-lookup"><span data-stu-id="7d727-511">You are now ready to start translating!</span></span>

## <a name="your-finished-translation-text-api-application"></a><span data-ttu-id="7d727-512">Votre application API de texte de traduction terminé</span><span class="sxs-lookup"><span data-stu-id="7d727-512">Your finished Translation Text API application</span></span>

<span data-ttu-id="7d727-513">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de traduction de texte Azure pour convertir la parole en texte traduit.</span><span class="sxs-lookup"><span data-stu-id="7d727-513">Congratulations, you built a mixed reality app that leverages the Azure Translation Text API to convert speech to translated text.</span></span>

![Produit final.](images/AzureLabs-Lab1-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="7d727-515">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="7d727-515">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="7d727-516">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="7d727-516">Exercise 1</span></span>

<span data-ttu-id="7d727-517">Pouvez-vous ajouter la fonctionnalité de conversion de texte par synthèse vocale à l’application, afin que le texte retourné soit parlé?</span><span class="sxs-lookup"><span data-stu-id="7d727-517">Can you add text-to-speech functionality to the app, so that the returned text is spoken?</span></span>

### <a name="exercise-2"></a><span data-ttu-id="7d727-518">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="7d727-518">Exercise 2</span></span>

<span data-ttu-id="7d727-519">Permet à l’utilisateur de modifier les langues source et de sortie («from» et «to») au sein de l’application elle-même, de sorte que l’application n’a pas besoin d’être reconstruite chaque fois que vous souhaitez modifier des langues.</span><span class="sxs-lookup"><span data-stu-id="7d727-519">Make it possible for the user to change the source and output languages ('from' and 'to') within the app itself, so the app does not need to be rebuilt every time you want to change languages.</span></span>
