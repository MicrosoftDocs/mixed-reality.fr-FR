---
title: MR et Azure 307-machine learning
description: Suivez ce cours pour apprendre à implémenter Azure Machine Learning Studio dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, Machine Learning, ml, Machine Learning Studio, hololens, immersif, VR
ms.openlocfilehash: c86c592573dd39d926869d8cce6025fa264cc90f
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437923"
---
>[!NOTE]
><span data-ttu-id="e93b8-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="e93b8-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="e93b8-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="e93b8-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="e93b8-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e93b8-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="e93b8-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="e93b8-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="e93b8-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="e93b8-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="e93b8-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="e93b8-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-307-machine-learning"></a><span data-ttu-id="e93b8-110">MR et Azure 307 : machine learning</span><span class="sxs-lookup"><span data-stu-id="e93b8-110">MR and Azure 307: Machine learning</span></span>

![produit final-début](images/AzureLabs-Lab7-0.png)

<span data-ttu-id="e93b8-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Machine Learning (ML) à une application de réalité mixte à l’aide d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e93b8-112">In this course, you will learn how to add Machine Learning (ML) capabilities to a mixed reality application using Azure Machine Learning Studio.</span></span>

<span data-ttu-id="e93b8-113">*Azure machine learning Studio* est un service Microsoft qui fournit aux développeurs un grand nombre d’algorithmes de machine learning, qui peuvent aider à l’entrée, à la sortie, à la préparation et à la visualisation des données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-113">*Azure Machine Learning Studio* is a Microsoft service, which provides developers with a large number of machine learning algorithms, which can help with data input, output, preparation, and visualization.</span></span> <span data-ttu-id="e93b8-114">À partir de ces composants, il est alors possible de développer une expérience d’analyse prédictive, d’effectuer une itération sur celle-ci et de l’utiliser pour former votre modèle.</span><span class="sxs-lookup"><span data-stu-id="e93b8-114">From these components, it is then possible to develop a predictive analytics experiment, iterate on it, and use it to train your model.</span></span> <span data-ttu-id="e93b8-115">Après la formation, vous pouvez rendre votre modèle opérationnel dans le Cloud Azure, afin qu’il puisse noter de nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-115">Following training, you can make your model operational within the Azure cloud, so that it can then score new data.</span></span> <span data-ttu-id="e93b8-116">Pour plus d’informations, consultez la [page Azure machine learning Studio](https://azure.microsoft.com/services/machine-learning-studio/).</span><span class="sxs-lookup"><span data-stu-id="e93b8-116">For more information, visit the [Azure Machine Learning Studio page](https://azure.microsoft.com/services/machine-learning-studio/).</span></span>

<span data-ttu-id="e93b8-117">Après avoir terminé ce cours, vous disposerez d’une application de casque d’immersion en réalité mixte et vous aurez appris comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e93b8-117">Having completed this course, you will have a mixed reality immersive headset application, and will have learned how do the following:</span></span>

1.  <span data-ttu-id="e93b8-118">Fournissez une table de données de ventes au portail *Azure machine learning Studio* et concevez un algorithme pour prédire les ventes futures d’éléments populaires.</span><span class="sxs-lookup"><span data-stu-id="e93b8-118">Provide a table of sales data to the *Azure Machine Learning Studio* portal, and        design an algorithm to predict future sales of popular items.</span></span>
2.  <span data-ttu-id="e93b8-119">Créez un **projet Unity**, qui peut recevoir et interpréter les données de prédiction du service ml.</span><span class="sxs-lookup"><span data-stu-id="e93b8-119">Create a **Unity Project**, which can receive and interpret prediction data from the ML service.</span></span>
3.  <span data-ttu-id="e93b8-120">Affichez les données de prédicat visuellement dans le **projet Unity**, en fournissant les Articles de vente les plus populaires sur une étagère.</span><span class="sxs-lookup"><span data-stu-id="e93b8-120">Display the predication data visually within the **Unity Project**, through providing the most popular sales items, on a shelf.</span></span>

<span data-ttu-id="e93b8-121">Dans votre application, c’est à vous de savoir comment vous allez intégrer les résultats à votre conception.</span><span class="sxs-lookup"><span data-stu-id="e93b8-121">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="e93b8-122">Ce cours est conçu pour vous apprendre à intégrer un service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="e93b8-122">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="e93b8-123">C’est votre travail d’utiliser les connaissances que vous avez acquises dans ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="e93b8-123">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

<span data-ttu-id="e93b8-124">Ce cours est un didacticiel autonome qui n’implique pas directement d’autres laboratoires de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="e93b8-124">This course is a self-contained tutorial, which does not directly involve any other Mixed Reality Labs.</span></span>

## <a name="device-support"></a><span data-ttu-id="e93b8-125">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="e93b8-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="e93b8-126">Course</span><span class="sxs-lookup"><span data-stu-id="e93b8-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="e93b8-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="e93b8-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="e93b8-128"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="e93b8-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="e93b8-129">MR et Azure 307 : machine learning</span><span class="sxs-lookup"><span data-stu-id="e93b8-129">MR and Azure 307: Machine learning</span></span></td><td style="text-align: center;"> <span data-ttu-id="e93b8-130">✔️</span><span class="sxs-lookup"><span data-stu-id="e93b8-130">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="e93b8-131">✔️</span><span class="sxs-lookup"><span data-stu-id="e93b8-131">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="e93b8-132">Bien que ce cours se concentre principalement sur les casques de Windows Mixed Reality (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours à Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e93b8-132">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="e93b8-133">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge HoloLens.</span><span class="sxs-lookup"><span data-stu-id="e93b8-133">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="e93b8-134">Lorsque vous utilisez HoloLens, vous remarquerez peut-être un écho pendant la capture vocale.</span><span class="sxs-lookup"><span data-stu-id="e93b8-134">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e93b8-135">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="e93b8-135">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="e93b8-136">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="e93b8-136">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="e93b8-137">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="e93b8-137">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="e93b8-138">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l' [article installer les outils](install-the-tools.md), bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="e93b8-138">You are free to use the latest software, as listed within the [install the tools article](install-the-tools.md), though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="e93b8-139">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours :</span><span class="sxs-lookup"><span data-stu-id="e93b8-139">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="e93b8-140">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="e93b8-140">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="e93b8-141">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="e93b8-141">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e93b8-142">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="e93b8-142">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e93b8-143">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="e93b8-143">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="e93b8-144">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="e93b8-144">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="e93b8-145">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="e93b8-145">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="e93b8-146">Accès Internet pour l’installation d’Azure et la récupération de données ML</span><span class="sxs-lookup"><span data-stu-id="e93b8-146">Internet access for Azure setup and ML data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="e93b8-147">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="e93b8-147">Before you start</span></span>

<span data-ttu-id="e93b8-148">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="e93b8-148">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span> 

## <a name="chapter-1---azure-storage-account-setup"></a><span data-ttu-id="e93b8-149">Chapitre 1-Configuration d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="e93b8-149">Chapter 1 - Azure Storage Account setup</span></span>

<span data-ttu-id="e93b8-150">Pour utiliser l’API Azure translator, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="e93b8-150">To use the Azure Translator API, you will need to configure an instance of the service to be made available to your application.</span></span>
1.  <span data-ttu-id="e93b8-151">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e93b8-151">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="e93b8-152">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="e93b8-152">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="e93b8-153">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="e93b8-153">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="e93b8-154">Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="e93b8-154">Once you are logged in, click on **Storage Accounts** in the left menu.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-1.png)

    > [!NOTE]
    > <span data-ttu-id="e93b8-156">Le mot **nouveau** peut avoir été remplacé par **créer une ressource**, dans les portails plus récents.</span><span class="sxs-lookup"><span data-stu-id="e93b8-156">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="e93b8-157">Dans l’onglet **comptes de stockage** , cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-157">On the **Storage Accounts** tab, click on **Add**.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-2.png)

4.  <span data-ttu-id="e93b8-159">Dans le panneau **créer un compte de stockage** :</span><span class="sxs-lookup"><span data-stu-id="e93b8-159">In the **Create Storage Account** panel:</span></span>

    1.  <span data-ttu-id="e93b8-160">Insérez un **nom** pour votre compte. n’oubliez pas que ce champ accepte uniquement des chiffres et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="e93b8-160">Insert a **Name** for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>
    2.  <span data-ttu-id="e93b8-161">Pour **modèle de déploiement,** sélectionnez **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-161">For **Deployment model,** select **Resource manager**.</span></span>
    3.  <span data-ttu-id="e93b8-162">Pour **type de compte**, sélectionnez **stockage (à usage général v1)** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-162">For **Account kind**, select **Storage (general purpose v1)**.</span></span>
    4.  <span data-ttu-id="e93b8-163">Pour **performances**, sélectionnez **standard**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-163">For **Performance**, select **Standard**.</span></span>
    5.  <span data-ttu-id="e93b8-164">Pour **la réplication** , sélectionnez **Read-Access-géo-redondant Storage (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-164">For **Replication** select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>
    6.  <span data-ttu-id="e93b8-165">Laissez le **transfert sécurisé requis** comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-165">Leave **Secure transfer required** as **Disabled**.</span></span>
    7.  <span data-ttu-id="e93b8-166">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-166">Select a **Subscription**.</span></span>
    4. <span data-ttu-id="e93b8-167">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e93b8-167">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="e93b8-168">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e93b8-168">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="e93b8-169">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="e93b8-169">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="e93b8-170">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="e93b8-170">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>
    
    5.  <span data-ttu-id="e93b8-171">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="e93b8-171">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="e93b8-172">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="e93b8-172">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="e93b8-173">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="e93b8-173">Some Azure assets are only available in certain regions.</span></span>

5.  <span data-ttu-id="e93b8-174">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-174">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-3.png)

6.  <span data-ttu-id="e93b8-176">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="e93b8-176">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="e93b8-177">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-177">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Configuration du compte de stockage Azure](images/AzureLabs-Lab7-4.png)

## <a name="chapter-2---the-azure-machine-learning-studio"></a><span data-ttu-id="e93b8-179">Chapitre 2-Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="e93b8-179">Chapter 2 - The Azure Machine Learning Studio</span></span>

<span data-ttu-id="e93b8-180">Pour utiliser l' *Azure machine learning*, vous devez configurer une instance du service machine learning à mettre à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="e93b8-180">To use the *Azure Machine Learning*, you will need to configure an instance of the Machine Learning service to be made available to your application.</span></span>

1.  <span data-ttu-id="e93b8-181">Dans le portail Azure, cliquez sur **nouveau** dans l’angle supérieur gauche et recherchez **machine learning Studio espace de travail**, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-181">In the Azure Portal, click on **New** in the top left corner, and search for **Machine Learning Studio Workspace**, press **Enter**.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-5.png)

2.  <span data-ttu-id="e93b8-183">La nouvelle page fournit une description du service d' **espace de travail machine learning Studio** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-183">The new page will provide a description of the **Machine Learning Studio Workspace**  service.</span></span> <span data-ttu-id="e93b8-184">En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-184">At the bottom left of this prompt, click the **Create** button, to create an association with this service.</span></span>

3.  <span data-ttu-id="e93b8-185">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche pour vous permettre de fournir des détails sur votre nouveau **service machine learning Studio**:</span><span class="sxs-lookup"><span data-stu-id="e93b8-185">Once you have clicked on **Create**, a panel will appear where you need to provide some details about your new **Machine Learning Studio service**:</span></span>

    1.  <span data-ttu-id="e93b8-186">Insérez le nom de l' **espace de travail** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-186">Insert your desired **Workspace name** for this service instance.</span></span>

    2.  <span data-ttu-id="e93b8-187">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-187">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="e93b8-188">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="e93b8-188">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="e93b8-189">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e93b8-189">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="e93b8-190">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces laboratoires) sous un groupe de ressources commun).</span><span class="sxs-lookup"><span data-stu-id="e93b8-190">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="e93b8-191">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="e93b8-191">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="e93b8-192">Déterminez l' **emplacement** de votre groupe de ressources (si vous créez un groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="e93b8-192">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="e93b8-193">L’emplacement devrait idéalement se trouver dans la région où l’application s’exécutait.</span><span class="sxs-lookup"><span data-stu-id="e93b8-193">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="e93b8-194">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="e93b8-194">Some Azure assets are only available in certain regions.</span></span> <span data-ttu-id="e93b8-195">Vous devez utiliser le même groupe de ressources que celui que vous avez utilisé pour créer le stockage Azure dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="e93b8-195">You should use the same resource group that you used for creating the Azure Storage in the previous Chapter.</span></span>

    5.  <span data-ttu-id="e93b8-196">Pour la section **compte de stockage** , cliquez sur utiliser l' **existant**, puis cliquez sur le menu déroulant, et à partir de là, cliquez sur le compte de **stockage** que vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="e93b8-196">For the **Storage account** section, click **Use existing**, then click the dropdown menu, and from there, click the **Storage Account** you created in the last Chapter.</span></span>

    6.  <span data-ttu-id="e93b8-197">Sélectionnez le **niveau tarifaire** de l’espace de travail approprié dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="e93b8-197">Select the appropriate **Workspace pricing tier** for you, from the dropdown menu.</span></span>

    7.  <span data-ttu-id="e93b8-198">Dans la section **plan de service Web** , cliquez sur **créer** **nouveau,** puis insérez un nom dans le champ de texte.</span><span class="sxs-lookup"><span data-stu-id="e93b8-198">Within the **Web service plan** section, click **Create** **new,** then insert a name for it in the text field.</span></span>

    8.  <span data-ttu-id="e93b8-199">Dans la section **niveau tarifaire du plan de service Web** , sélectionnez le niveau tarifaire de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e93b8-199">From the **Web service plan pricing tier** section, select the price tier of your choice.</span></span> <span data-ttu-id="e93b8-200">Un niveau de test de développement appelé **DEVTEST standard** doit être disponible gratuitement.</span><span class="sxs-lookup"><span data-stu-id="e93b8-200">A development testing tier called **DEVTEST Standard** should be available to you at no charge.</span></span>

    9.  <span data-ttu-id="e93b8-201">Vous devrez également confirmer que vous avez compris les conditions générales appliquées à ce service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-201">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    10. <span data-ttu-id="e93b8-202">Cliquez sur **Create (Créer)** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-202">Click **Create**.</span></span>

        ![Azure Machine Learning Studio](images/AzureLabs-Lab7-6.png)

4.  <span data-ttu-id="e93b8-204">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="e93b8-204">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

5.  <span data-ttu-id="e93b8-205">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-205">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-7.png)

6.  <span data-ttu-id="e93b8-207">Cliquez sur la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-207">Click on the notification to explore your new Service instance.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-8.png)

7.  <span data-ttu-id="e93b8-209">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-209">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span>

8.  <span data-ttu-id="e93b8-210">Dans la page qui s’affiche, sous la section **liens supplémentaires** , cliquez sur **lancer machine learning Studio**, ce qui permet de diriger votre navigateur vers le portail des **machine learning Studio** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-210">In the page displayed, under the **Additional Links** section, click **Launch Machine Learning Studio**, which will direct your browser to the **Machine Learning Studio** portal.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-9.png)

9.  <span data-ttu-id="e93b8-212">Utilisez le bouton **se connecter** , en haut à droite ou au centre, pour vous connecter à votre machine learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e93b8-212">Use the **Sign In** button, at the top right or in the center, to log into your Machine Learning Studio.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-10.png)


## <a name="chapter-3---the-machine-learning-studio-dataset-setup"></a><span data-ttu-id="e93b8-214">Chapitre 3-Machine Learning Studio : installation du jeu de données</span><span class="sxs-lookup"><span data-stu-id="e93b8-214">Chapter 3 - The Machine Learning Studio: Dataset setup</span></span>

<span data-ttu-id="e93b8-215">L’une des méthodes Machine Learning fonctionnement des algorithmes consiste à analyser les données existantes et à essayer de prédire les résultats futurs en fonction du jeu de données existant.</span><span class="sxs-lookup"><span data-stu-id="e93b8-215">One of the ways Machine Learning algorithms work is by analyzing existing data and then attempting to predict future results based on the existing data set.</span></span> <span data-ttu-id="e93b8-216">Cela signifie généralement que plus vous avez de données existantes, plus l’algorithme sera adapté à la prévision des résultats futurs.</span><span class="sxs-lookup"><span data-stu-id="e93b8-216">This generally means that the more existing data you have, the better the algorithm will be at predicting future results.</span></span>

<span data-ttu-id="e93b8-217">Un exemple de table est fourni pour vous, dans le cadre de ce cours, appelé [ProductsTableCSV et peut être téléchargé ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).</span><span class="sxs-lookup"><span data-stu-id="e93b8-217">A sample table is provided to you, for this course, called [ProductsTableCSV and can be downloaded here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e93b8-218">Le fichier. zip ci-dessus contient à la fois **ProductsTableCSV** et **. pour Unity**, dont vous aurez besoin au [chapitre 6](#chapter-6---importing-the-mlproducts-unity-package).</span><span class="sxs-lookup"><span data-stu-id="e93b8-218">The above .zip file contains both the **ProductsTableCSV** and the **.unitypackage**, which you will need in [Chapter 6](#chapter-6---importing-the-mlproducts-unity-package).</span></span> <span data-ttu-id="e93b8-219">Ce package est également fourni dans ce chapitre, bien qu’il soit séparé par le fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="e93b8-219">This package is also provided within that Chapter, though separate to the csv file.</span></span>

<span data-ttu-id="e93b8-220">Cet exemple de jeu de données contient un enregistrement des objets les plus vendus à chaque heure de chaque jour de l’année 2017.</span><span class="sxs-lookup"><span data-stu-id="e93b8-220">This sample data set contains a record of the best-selling objects at every hour of each day of the year 2017.</span></span>
        
![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-11.png)

<span data-ttu-id="e93b8-222">Par exemple, le jour 1 de 2017, à 13h00 (heure 13), l’article le mieux vendu était sel et poivron.</span><span class="sxs-lookup"><span data-stu-id="e93b8-222">For example, on day 1 of 2017, at 1pm (hour 13), the best-selling item was salt and pepper.</span></span>

<span data-ttu-id="e93b8-223">Cet exemple de table contient 9998 entrées.</span><span class="sxs-lookup"><span data-stu-id="e93b8-223">This sample table contains 9998 entries.</span></span>

1.  <span data-ttu-id="e93b8-224">Revenez au portail **machine learning Studio** et ajoutez ce tableau en tant que **jeu de données** pour votre ml.</span><span class="sxs-lookup"><span data-stu-id="e93b8-224">Head back to the **Machine Learning Studio** portal, and add this table as a **Dataset** for your ML.</span></span> <span data-ttu-id="e93b8-225">Pour ce faire, cliquez sur le bouton **+ nouveau** dans le coin inférieur gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="e93b8-225">Do this by clicking the **+ New** button in the bottom left corner of the screen.</span></span>

    ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-12.png)

2.  <span data-ttu-id="e93b8-227">Une section s’affiche à partir du bas et, dans la partie gauche du panneau de navigation.</span><span class="sxs-lookup"><span data-stu-id="e93b8-227">A section will come up from the bottom, and within that there is navigation panel on the left.</span></span> <span data-ttu-id="e93b8-228">Cliquez sur **DataSet**, puis à droite de celui-ci, **à partir du fichier local**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-228">Click **Dataset**, then to the right of that, **From Local File**.</span></span>

    ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-13.png)

3.  <span data-ttu-id="e93b8-230">Téléchargez le nouveau **jeu de données** en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="e93b8-230">Upload the new **Dataset** by following these steps:</span></span>

    1. <span data-ttu-id="e93b8-231">La fenêtre de chargement s’affiche, dans laquelle vous pouvez **Parcourir** votre disque dur pour le nouveau jeu de données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-231">The upload window will appear, where you can **Browse** your hard drive for the new dataset.</span></span>

        ![Machine Learning Studio : configuration du jeu de données](images/AzureLabs-Lab7-14.png)

    2.  <span data-ttu-id="e93b8-233">Une fois que vous avez sélectionné, puis de nouveau dans la fenêtre de chargement, laissez la case à cocher désactivée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-233">Once selected, and back in the upload window, leave the checkbox unticked.</span></span>

    3.  <span data-ttu-id="e93b8-234">Dans le champ de texte ci-dessous, entrez **ProductsTableCSV. csv** comme nom du jeu de données (bien qu’il soit ajouté automatiquement).</span><span class="sxs-lookup"><span data-stu-id="e93b8-234">In the text field below, enter **ProductsTableCSV.csv** as the name for the dataset (though should automatically be added).</span></span>

    4.  <span data-ttu-id="e93b8-235">Dans le menu déroulant **type**, sélectionnez **fichier CSV générique avec un en-tête (. csv)** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-235">Using the dropdown menu for **Type**, select **Generic CSV File with a header (.csv)**.</span></span>

    5.  <span data-ttu-id="e93b8-236">Appuyez sur la coche dans le coin inférieur droit de la fenêtre de chargement pour charger votre **jeu de données** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-236">Press the tick in the bottom right of the upload window, and your **Dataset** will be uploaded.</span></span>

## <a name="chapter-4---the-machine-learning-studio-the-experiment"></a><span data-ttu-id="e93b8-237">Chapitre 4-Machine Learning Studio : l’expérience</span><span class="sxs-lookup"><span data-stu-id="e93b8-237">Chapter 4 - The Machine Learning Studio: The Experiment</span></span>

<span data-ttu-id="e93b8-238">Avant de pouvoir créer votre système Machine Learning, vous devrez créer une expérience pour valider votre théorie sur vos données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-238">Before you can build your machine learning system, you will need to build an experiment, to validate your theory about your data.</span></span> <span data-ttu-id="e93b8-239">Avec les résultats, vous saurez si vous avez besoin de davantage de données, ou s’il n’existe aucune corrélation entre les données et un résultat possible.</span><span class="sxs-lookup"><span data-stu-id="e93b8-239">With the results, you will know whether you need more data, or if there is no correlation between the data and a possible outcome.</span></span>

<span data-ttu-id="e93b8-240">Pour commencer à créer une expérience :</span><span class="sxs-lookup"><span data-stu-id="e93b8-240">To start creating an experiment:</span></span>

1.  <span data-ttu-id="e93b8-241">Cliquez à nouveau sur le bouton **+ nouveau** en bas à gauche de la page, puis cliquez sur **expérience** > **expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-241">Click again on the **+ New** button on the bottom left of the page, then click on **Experiment** > **Blank Experiment**.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-15.png)

2.  <span data-ttu-id="e93b8-243">Une nouvelle page s’affiche avec une expérience vide :</span><span class="sxs-lookup"><span data-stu-id="e93b8-243">A new page will be displayed with a blank Experiment:</span></span>

3.  <span data-ttu-id="e93b8-244">Dans le volet de gauche, développez **DataSets enregistrés** > **mes jeux de données** , puis faites glisser le **ProductsTableCSV** dans la **zone de dessin**de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-244">From the panel on the left expand **Saved Datasets** > **My Datasets** and drag the  **ProductsTableCSV** on to the **Experiment Canvas**.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-16.png)

4.  <span data-ttu-id="e93b8-246">Dans le volet de gauche, développez **transformation des données** > **échantillon et fractionner**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-246">In the panel on the left, expand **Data Transformation** > **Sample and Split**.</span></span> <span data-ttu-id="e93b8-247">Ensuite, faites glisser l’élément **fractionner les données** dans la **zone de dessin**de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-247">Then drag the **Split Data** item in to the **Experiment Canvas**.</span></span> <span data-ttu-id="e93b8-248">L’élément fractionner les données divise le jeu de données en deux parties.</span><span class="sxs-lookup"><span data-stu-id="e93b8-248">The Split Data item will split the data set into two parts.</span></span> <span data-ttu-id="e93b8-249">Une partie que vous allez utiliser pour l’apprentissage de l’algorithme Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e93b8-249">One part you will use for training the machine learning algorithm.</span></span> <span data-ttu-id="e93b8-250">La deuxième partie sera utilisée pour évaluer la précision de l’algorithme généré.</span><span class="sxs-lookup"><span data-stu-id="e93b8-250">The second part will be used to evaluate the accuracy of the algorithm generated.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-17.png)

5.  <span data-ttu-id="e93b8-252">Dans le volet droit (tandis que l’élément fractionner les données sur le canevas est sélectionné), modifiez la **fraction des lignes du premier jeu** de données de sortie sur **0,7**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-252">In the right panel (while the Split Data item on the canvas is selected), edit the **Fraction of rows in the first output dataset** to **0.7**.</span></span> <span data-ttu-id="e93b8-253">Cela répartit les données en deux parties, la première partie est de 70% des données, et la deuxième partie sera les 30% restants.</span><span class="sxs-lookup"><span data-stu-id="e93b8-253">This will split the data into two parts, the first part will be 70% of the data, and the second part will be the remaining 30%.</span></span> <span data-ttu-id="e93b8-254">Pour vous assurer que les données sont fractionnées de façon aléatoire, assurez-vous que la case à cocher **fractionnement aléatoire** reste activée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-254">To ensure that the data is split randomly, make sure the **Randomized split** checkbox remains checked.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-18.png)

6.  <span data-ttu-id="e93b8-256">Faites glisser une connexion de la base de l’élément **ProductsTableCSV** sur la zone de dessin vers le haut de l’élément de données fractionnées.</span><span class="sxs-lookup"><span data-stu-id="e93b8-256">Drag a connection from the base of the **ProductsTableCSV** item on the canvas to the top of the Split Data item.</span></span> <span data-ttu-id="e93b8-257">Cela permet de connecter les éléments et d’envoyer la sortie du jeu de données **ProductsTableCSV** (les données) à l’entrée de fractionnement des données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-257">This will connect the items and send the **ProductsTableCSV** dataset output (the data) to the Split Data input.</span></span>  

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-19.png)

7.  <span data-ttu-id="e93b8-259">Dans le panneau **expériences** sur le côté gauche, développez **machine learning** > **train**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-259">In the **Experiments** panel on the left side, expand **Machine Learning** > **Train**.</span></span> <span data-ttu-id="e93b8-260">Faites glisser l’élément **former le modèle** dans la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-260">Drag the **Train Model** item out in to the Experiment canvas.</span></span> <span data-ttu-id="e93b8-261">Votre canevas doit ressembler à ce qui suit.</span><span class="sxs-lookup"><span data-stu-id="e93b8-261">Your canvas should look the same as the below.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-20.png)

8.  <span data-ttu-id="e93b8-263">En ***bas à gauche*** de l’élément de **données fractionnées** , faites glisser une connexion en **haut à droite** de l’élément former le **modèle** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-263">From the ***bottom left*** of the **Split Data** item drag a connection to the **top right** of the **Train Model** item.</span></span> <span data-ttu-id="e93b8-264">La première division de 70% du jeu de données sera utilisée par le modèle de formation pour former l’algorithme.</span><span class="sxs-lookup"><span data-stu-id="e93b8-264">The first 70% split from the dataset will be used by the Train Model to train the algorithm.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-21.png)

9.  <span data-ttu-id="e93b8-266">Sélectionnez l’élément **former le modèle** sur la zone de dessin, puis dans le panneau **Propriétés** (sur le côté droit de la fenêtre de votre navigateur), cliquez sur le bouton lancer le **Sélecteur de colonne** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-266">Select the **Train Model** item on the canvas, and in the **Properties** panel (on the right-hand side of your browser window) click the **Launch column selector** button.</span></span>

10. <span data-ttu-id="e93b8-267">Dans la zone de texte type **Product** , puis appuyez sur **entrée**, *Product* sera défini en tant que colonne pour former des prédictions.</span><span class="sxs-lookup"><span data-stu-id="e93b8-267">In the text box type **product** and then press **Enter**, *product* will be set as a column to train predictions.</span></span> <span data-ttu-id="e93b8-268">Ensuite, cliquez sur la **coche** dans le coin inférieur droit pour fermer la boîte de dialogue de sélection.</span><span class="sxs-lookup"><span data-stu-id="e93b8-268">Following this, click on the **tick** in the bottom-right corner to close the selection dialog.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-22.png)

11. <span data-ttu-id="e93b8-270">Vous allez former un algorithme de **régression logistique multiclasse** afin de prédire le **produit** le plus vendu en fonction de l’heure de la journée et de la date.</span><span class="sxs-lookup"><span data-stu-id="e93b8-270">You are going to train a **Multiclass Logistic Regression** algorithm to predict the most sold **product** based on the hour of the day and the date.</span></span> <span data-ttu-id="e93b8-271">L’explication des différents algorithmes fournis par le Azure Machine Learning Studio n’entre pas dans le cadre de ce document. Toutefois, vous pouvez en savoir plus sur l’aide-mémoire de l' [algorithme machine learning](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)</span><span class="sxs-lookup"><span data-stu-id="e93b8-271">It is beyond the scope of this document to explain the details of the different algorithms provided by the Azure Machine Learning studio, though, you can find out more from the [Machine Learning Algorithm Cheat Sheet](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)</span></span>

12. <span data-ttu-id="e93b8-272">Dans le panneau des éléments d’expérience sur la gauche, développez **Machine Learning** > **initialiser le modèle** > **classification**, puis faites glisser l’élément **multiCLASS logistique Regression** sur la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-272">From the experiment items panel on the left, expand **Machine Learning** > **Initialize Model** > **Classification**, and drag the **Multiclass Logistic Regression** item on to the experiment canvas.</span></span>

13. <span data-ttu-id="e93b8-273">Connectez la sortie, en bas de la **régression logistique multiclasse**, à l’entrée en haut à gauche de l’élément de **modèle de formation** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-273">Connect the output, from the bottom of the **Multiclass Logistic Regression**, to the top-left input of the **Train Model** item.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-23.png)

14. <span data-ttu-id="e93b8-275">Dans la liste des éléments d’expérience dans le panneau de gauche, développez **Machine Learning** > **score**, puis faites glisser l’élément de **modèle de score** sur le canevas.</span><span class="sxs-lookup"><span data-stu-id="e93b8-275">In list of experiment items in the panel on the left, expand **Machine Learning** > **Score**, and drag the **Score Model** item on to the canvas.</span></span>

15. <span data-ttu-id="e93b8-276">Connectez la sortie, du bas du modèle de **formation**, à l’entrée en haut à gauche du **modèle de score**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-276">Connect the output, from the bottom of the **Train Model**, to the top-left input of the **Score Model**.</span></span>

16. <span data-ttu-id="e93b8-277">Connectez la sortie en bas à droite à partir des **données de fractionnement**à l’entrée en haut à droite de l’élément de **modèle de score** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-277">Connect the bottom-right output from **Split Data**, to the top-right input of the **Score Model** item.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-24.png)

17. <span data-ttu-id="e93b8-279">Dans la liste des éléments d' **expérience** dans le volet gauche, développez **machine learning** > **évaluer**, puis faites glisser l’élément de **modèle Evaluate** sur le canevas.</span><span class="sxs-lookup"><span data-stu-id="e93b8-279">In the list of **Experiment** items in the panel on the left, expand **Machine Learning** > **Evaluate**, and drag the **Evaluate Model** item onto the canvas.</span></span>

18. <span data-ttu-id="e93b8-280">Connectez la sortie du **modèle de score** à l’entrée située en haut à gauche du **modèle d’évaluation**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-280">Connect the output from the **Score Model** to the top-left input of the **Evaluate Model**.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-25.png)

19. <span data-ttu-id="e93b8-282">Vous avez créé votre première expérience Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e93b8-282">You have built your first Machine Learning Experiment.</span></span> <span data-ttu-id="e93b8-283">Vous pouvez maintenant enregistrer et exécuter l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-283">You can now save and run the experiment.</span></span> <span data-ttu-id="e93b8-284">Dans le menu situé en bas de la page, cliquez sur le bouton **Enregistrer** pour enregistrer votre expérience, puis cliquez sur **exécuter** jusqu’au début de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-284">In the menu at the bottom of the page, click on the **Save** button to save your experiment and then click **Run** to the start the experiment.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-26.png)

20. <span data-ttu-id="e93b8-286">Vous pouvez voir l' **État** de l’expérience dans l’angle supérieur droit de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="e93b8-286">You can see the **status** of the experiment in the top-right of the canvas.</span></span> <span data-ttu-id="e93b8-287">Attendez quelques instants que l’expérience se termine.</span><span class="sxs-lookup"><span data-stu-id="e93b8-287">Wait a few moments for the experiment to finish.</span></span>

    > <span data-ttu-id="e93b8-288">Si vous avez un jeu de données volumineux (réel), il est probable que l’expérience peut prendre plusieurs heures.</span><span class="sxs-lookup"><span data-stu-id="e93b8-288">If you have a big (real world) dataset it is likely that the experiment could take hours to run.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-27.png)

21. <span data-ttu-id="e93b8-290">Cliquez avec le bouton droit sur l’élément de **modèle Evaluate** dans le canevas, puis, dans le menu contextuel, pointez avec la souris sur résultats de l' **évaluation**, puis sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-290">Right click on the **Evaluate Model** item in the canvas and from the context menu hover the mouse over **Evaluation Results**, then select **Visualize**.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-28.png)

22. <span data-ttu-id="e93b8-292">Les résultats de l’évaluation s’affichent et indiquent les résultats prédits par rapport aux résultats réels.</span><span class="sxs-lookup"><span data-stu-id="e93b8-292">The evaluation results will be displayed showing the predicted outcomes versus the actual outcomes.</span></span> <span data-ttu-id="e93b8-293">Cela utilise les 30% du jeu de données d’origine, qui a été divisé précédemment, pour l’évaluation du modèle.</span><span class="sxs-lookup"><span data-stu-id="e93b8-293">This uses the 30% of the original dataset, that was split earlier, for evaluating the model.</span></span> <span data-ttu-id="e93b8-294">Vous pouvez voir que les résultats ne sont pas excellents. dans l’idéal, le nombre le plus élevé dans chaque ligne est l’élément mis en surbrillance dans les colonnes.</span><span class="sxs-lookup"><span data-stu-id="e93b8-294">You can see the results are not great, ideally you would have the highest number in each row be the highlighted item in the columns.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-29.png)

23. <span data-ttu-id="e93b8-296">Fermez les **résultats**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-296">Close the **Results**.</span></span>

24. <span data-ttu-id="e93b8-297">Pour utiliser votre modèle de Machine Learning nouvellement formé, vous devez l’exposer en tant que **service Web**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-297">To use your newly trained Machine Learning model you need to expose it as a **Web Service**.</span></span> <span data-ttu-id="e93b8-298">Pour ce faire, cliquez sur l’élément de menu **configurer le service Web** dans le menu situé en bas de la page, puis cliquez sur **service Web prédictif**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-298">To do this, click on the **Set Up Web Service** menu item in the menu at the bottom of the page, and click on **Predictive Web Service**.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-30.png)

25. <span data-ttu-id="e93b8-300">Un nouvel onglet est créé, et le modèle de formation est fusionné pour créer le nouveau service Web.</span><span class="sxs-lookup"><span data-stu-id="e93b8-300">A new tab will be created, and the train model merged to create the new web service.</span></span> 

26. <span data-ttu-id="e93b8-301">Dans le menu situé en bas de la page, cliquez sur **Enregistrer**, puis sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-301">In the menu at the bottom of the page click **Save**, then click **Run**.</span></span> <span data-ttu-id="e93b8-302">L’État mis à jour s’affiche dans l’angle supérieur droit de la zone de dessin de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="e93b8-302">You will see the status updated in the top-right corner of the experiment canvas.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-31.png)

27. <span data-ttu-id="e93b8-304">Une fois l’exécution terminée, un bouton **déployer le service Web** s’affiche en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="e93b8-304">Once it has finished running, a **Deploy Web Service** button will appear at the bottom of the page.</span></span> <span data-ttu-id="e93b8-305">Vous êtes prêt à déployer le service Web.</span><span class="sxs-lookup"><span data-stu-id="e93b8-305">You are ready to deploy the web service.</span></span> <span data-ttu-id="e93b8-306">Cliquez sur **déployer le service Web** (classique) dans le menu situé en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="e93b8-306">Click **Deploy Web Service** (Classic) in the menu at the bottom of the page.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-32.png)

    > <span data-ttu-id="e93b8-308">Votre navigateur peut demander à autoriser une fenêtre contextuelle, que vous devez **autoriser**, bien que vous deviez cliquer à nouveau sur **déployer le service Web** , si la page déployer ne s’affiche pas.</span><span class="sxs-lookup"><span data-stu-id="e93b8-308">Your browser may prompt to allow a pop-up, which you should **allow**, though you may need to press **Deploy Web Service** again, if the deploy page does not show.</span></span> 

28. <span data-ttu-id="e93b8-309">Une fois l’expérience créée, vous êtes redirigé vers une page du **tableau de bord** où votre **clé API** sera affichée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-309">Once the Experiment has been created you will be redirected to a **Dashboard** page where you will have your **API Key** displayed.</span></span> <span data-ttu-id="e93b8-310">Copiez-la dans un bloc-notes pour le moment. vous en aurez besoin dans votre code très rapidement.</span><span class="sxs-lookup"><span data-stu-id="e93b8-310">Copy it into a notepad for the moment, you will need it in your code very soon.</span></span> <span data-ttu-id="e93b8-311">Une fois que vous avez noté votre clé API, cliquez sur le bouton **requête/réponse** dans la section **point de terminaison par défaut** sous la clé.</span><span class="sxs-lookup"><span data-stu-id="e93b8-311">Once you have noted your API Key, click on the **REQUEST/RESPONSE** button in the **Default Endpoint** section underneath the Key.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-33.png)

    > [!NOTE] 
    > <span data-ttu-id="e93b8-313">Si vous cliquez sur tester dans cette page, vous serez en mesure d’entrer les données d’entrée et d’afficher la sortie.</span><span class="sxs-lookup"><span data-stu-id="e93b8-313">If you click Test in this page, you will be able to enter input data and view the output.</span></span> <span data-ttu-id="e93b8-314">Entrez le **jour** et l' **heure**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-314">Enter the **day** and **hour**.</span></span> <span data-ttu-id="e93b8-315">Laissez l’entrée du **produit** vide.</span><span class="sxs-lookup"><span data-stu-id="e93b8-315">Leave the **product** entry blank.</span></span> <span data-ttu-id="e93b8-316">Cliquez ensuite sur le bouton **confirmer** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-316">Then click the **Confirm** button.</span></span> <span data-ttu-id="e93b8-317">La sortie en bas de la page affiche le JSON qui représente la probabilité que chaque produit soit le choix.</span><span class="sxs-lookup"><span data-stu-id="e93b8-317">The output on the bottom of the page will show the JSON representing the likelihood of each product being the choice.</span></span>

29. <span data-ttu-id="e93b8-318">Une nouvelle page Web s’ouvre, affichant les instructions et des exemples sur la structure de demande requise par le Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="e93b8-318">A new web page will open up, displaying the instructions and some examples about the Request structure required by the Machine Learning Studio.</span></span> <span data-ttu-id="e93b8-319">Copiez l' **URI de demande** affiché dans cette page dans votre bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e93b8-319">Copy the **Request URI** displayed in this page, into your notepad.</span></span>

    ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-34.png)

<span data-ttu-id="e93b8-321">Vous avez maintenant créé un système de Machine Learning qui fournit le produit le plus probable à vendre en fonction des données d’achat historiques, corrélées avec l’heure du jour et du jour de l’année.</span><span class="sxs-lookup"><span data-stu-id="e93b8-321">You have now built a machine learning system that provides the most likely product to be sold based on historical purchasing data, correlated with the time of the day and day of the year.</span></span>

<span data-ttu-id="e93b8-322">Pour appeler le service Web, vous aurez besoin de l’URL du point de terminaison de service et d’une clé API pour le service.</span><span class="sxs-lookup"><span data-stu-id="e93b8-322">To call the web service, you will need the URL for the service endpoint and an API Key for the service.</span></span> <span data-ttu-id="e93b8-323">Dans le menu supérieur, cliquez sur l’onglet **consommer** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-323">Click on the **Consume** tab, from the top menu.</span></span>

<span data-ttu-id="e93b8-324">La page informations sur la **consommation** affiche les informations dont vous aurez besoin pour appeler le service Web à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="e93b8-324">The **Consumption** Info page will display the information you will need to call the web service from your code.</span></span> <span data-ttu-id="e93b8-325">Effectuez une copie de la **clé primaire** et de l’URL **de requête-réponse** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-325">Take a copy of the **Primary Key** and the **Request-Response** URL.</span></span> <span data-ttu-id="e93b8-326">Vous en aurez besoin dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="e93b8-326">You will need these in the next Chapter.</span></span>

## <a name="chapter-5---setting-up-the-unity-project"></a><span data-ttu-id="e93b8-327">Chapitre 5-Configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="e93b8-327">Chapter 5 - Setting up the Unity Project</span></span>

<span data-ttu-id="e93b8-328">Configurez et testez votre casque immersif en réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="e93b8-328">Set up and test your Mixed Reality Immersive Headset.</span></span>

> [!NOTE]
>  <span data-ttu-id="e93b8-329">Vous n’aurez **pas** besoin de contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="e93b8-329">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="e93b8-330">Si vous avez besoin de la prise en charge de la configuration du casque immersif, cliquez [ici](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="e93b8-330">If you need support setting up the Immersive Headset, please click [HERE](https://support.microsoft.com/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="e93b8-331">Ouvrez **Unity** et créez un nouveau projet Unity appelé **Mr\_MachineLearning.**</span><span class="sxs-lookup"><span data-stu-id="e93b8-331">Open **Unity** and create a new Unity Project called **MR\_MachineLearning.**</span></span> <span data-ttu-id="e93b8-332">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-332">Make sure the project type is set to **3D**.</span></span>

2.  <span data-ttu-id="e93b8-333">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-333">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="e93b8-334">Accédez à **modifier** > **Préférences** puis, dans la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-334">Go to **Edit** > **Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="e93b8-335">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-335">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="e93b8-336">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-336">Close the **Preferences** window.</span></span>

3.  <span data-ttu-id="e93b8-337">Accédez ensuite à **fichier** > **paramètres de build** et basculez la plateforme sur **plateforme Windows universelle**, en cliquant sur le bouton changer de ***plateforme*** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-337">Next, go to **File** > **Build Settings** and switch the platform to **Universal Windows Platform**, by clicking on the ***Switch Platform*** button.</span></span>

4.  <span data-ttu-id="e93b8-338">Assurez-vous également que :</span><span class="sxs-lookup"><span data-stu-id="e93b8-338">Also make sure that:</span></span>

    1.  <span data-ttu-id="e93b8-339">L' **appareil cible** est défini sur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-339">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="e93b8-340">Pour Microsoft HoloLens, définissez **appareil cible** sur *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="e93b8-340">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="e93b8-341">Le **type de build** est **D3D**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-341">**Build Type** is set to **D3D**.</span></span>

    3.  <span data-ttu-id="e93b8-342">Le **SDK** est configuré sur le **dernier installé**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-342">**SDK** is set to **Latest installed**.</span></span>

    4.  <span data-ttu-id="e93b8-343">La **version de Visual Studio** est **installée sur le plus récent**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-343">**Visual Studio Version** is set to **Latest installed**.</span></span>

    5.  <span data-ttu-id="e93b8-344">La **génération et l’exécution** sont définies sur l' **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-344">**Build and Run** is set to **Local Machine**.</span></span>

    6.  <span data-ttu-id="e93b8-345">Ne vous inquiétez pas de définir des **scènes** pour le moment, car elles sont fournies plus tard.</span><span class="sxs-lookup"><span data-stu-id="e93b8-345">Do not worry about setting up **Scenes** right now, as these are provided later.</span></span>

    7.  <span data-ttu-id="e93b8-346">Les paramètres restants doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="e93b8-346">The remaining settings should be left as default for now.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab7-35.png)

5.  <span data-ttu-id="e93b8-348">Dans la fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-348">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span> 

6. <span data-ttu-id="e93b8-349">Dans ce volet, quelques paramètres doivent être vérifiés :</span><span class="sxs-lookup"><span data-stu-id="e93b8-349">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="e93b8-350">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="e93b8-350">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="e93b8-351">La **version du runtime** de **script** doit être **expérimentale** (équivalent .net 4,6)</span><span class="sxs-lookup"><span data-stu-id="e93b8-351">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent)</span></span>

        2. <span data-ttu-id="e93b8-352">Le **backend de script** doit être ***.net***</span><span class="sxs-lookup"><span data-stu-id="e93b8-352">**Scripting Backend** should be ***.NET***</span></span>

        3. <span data-ttu-id="e93b8-353">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="e93b8-353">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab7-36.png)

    2.  <span data-ttu-id="e93b8-355">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher :</span><span class="sxs-lookup"><span data-stu-id="e93b8-355">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="e93b8-356">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="e93b8-356">**InternetClient**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab7-37.png)

    3.  <span data-ttu-id="e93b8-358">Plus bas dans le panneau, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté</span><span class="sxs-lookup"><span data-stu-id="e93b8-358">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab7-38.png)

    

6.  <span data-ttu-id="e93b8-360">De retour dans les **paramètres de build** , les projets *Unity C#*  ne sont plus grisés. Cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="e93b8-360">Back in **Build Settings** *Unity C#* Projects is no longer greyed out; tick the checkbox next to this.</span></span> 

7.  <span data-ttu-id="e93b8-361">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="e93b8-361">Close the Build Settings window.</span></span>

8.  <span data-ttu-id="e93b8-362">Enregistrez votre projet (**fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="e93b8-362">Save your Project (**FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-6---importing-the-mlproducts-unity-package"></a><span data-ttu-id="e93b8-363">Chapitre 6-importation du package MLProducts Unity</span><span class="sxs-lookup"><span data-stu-id="e93b8-363">Chapter 6 - Importing the MLProducts Unity Package</span></span>

<span data-ttu-id="e93b8-364">Pour ce cours, vous devrez télécharger un package d’actifs Unity appelé [**Azure-Mr-307. pour Unity**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="e93b8-364">For this course, you will need to download a Unity Asset Package called [**Azure-MR-307.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage).</span></span> <span data-ttu-id="e93b8-365">Ce package est complété par une scène, avec tous les objets de ce prégénération, ce qui vous permet de vous concentrer sur son fonctionnement.</span><span class="sxs-lookup"><span data-stu-id="e93b8-365">This package comes complete with a scene, with all objects in that prebuilt, so you can focus on getting it all working.</span></span> <span data-ttu-id="e93b8-366">Le script **ShelfKeeper** est fourni, bien que ne contienne que les variables publiques, à des fins de structure de configuration de scène.</span><span class="sxs-lookup"><span data-stu-id="e93b8-366">The **ShelfKeeper** script is provided, though only holds the public variables, for the purpose of scene setup structure.</span></span> <span data-ttu-id="e93b8-367">Vous devrez effectuer toutes les autres sections.</span><span class="sxs-lookup"><span data-stu-id="e93b8-367">You will need to do all other sections.</span></span> 

<span data-ttu-id="e93b8-368">Pour importer ce package :</span><span class="sxs-lookup"><span data-stu-id="e93b8-368">To import this package:</span></span>

1.  <span data-ttu-id="e93b8-369">Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis cliquez sur **Importer un package, puis sur package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-369">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package, Custom Package**.</span></span>

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-39.png)

2.  <span data-ttu-id="e93b8-371">Utilisez le sélecteur de fichiers pour sélectionner le package **Azure-Mr-307. pour Unity** , puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-371">Use the file picker to select the **Azure-MR-307.unitypackage** package and click **Open**.</span></span>

3.  <span data-ttu-id="e93b8-372">La liste des composants de cet élément multimédia vous est présentée.</span><span class="sxs-lookup"><span data-stu-id="e93b8-372">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="e93b8-373">Confirmez l’importation en cliquant sur **Importer**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-373">Confirm the import by clicking **Import**.</span></span>

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-40.png)

4.  <span data-ttu-id="e93b8-375">Une fois l’importation terminée, vous remarquerez que certains nouveaux dossiers apparaissent dans le **panneau Projet**Unity.</span><span class="sxs-lookup"><span data-stu-id="e93b8-375">Once it has finished importing, you will notice that some new folders have appeared in your Unity **Project Panel**.</span></span> <span data-ttu-id="e93b8-376">Il s’agit des modèles 3D et des matériaux correspondants qui font partie de la scène prédéfinie sur laquelle vous allez travailler.</span><span class="sxs-lookup"><span data-stu-id="e93b8-376">Those are the 3D models and the respective materials that are part of the pre-made scene you will work on.</span></span> <span data-ttu-id="e93b8-377">Vous allez écrire la majorité du code dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="e93b8-377">You will write the majority of the code in this course.</span></span>

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-41.png)

5.  <span data-ttu-id="e93b8-379">Dans le dossier du **panneau Projet** , cliquez sur le dossier **scenes** , puis double-cliquez sur la scène dans (appelée **MR_MachineLearningScene**).</span><span class="sxs-lookup"><span data-stu-id="e93b8-379">Within the **Project Panel** folder, click on the **Scenes** folder and double click on the scene inside (called **MR_MachineLearningScene**).</span></span> <span data-ttu-id="e93b8-380">La scène s’ouvre (Voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="e93b8-380">The scene will open (see image below).</span></span> <span data-ttu-id="e93b8-381">Si les losanges rouges sont manquants, cliquez simplement sur le bouton **gizmos** , en haut à droite du **panneau du jeu**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-381">If the red diamonds are missing, simply click the **Gizmos** button, at the top right of the **Game Panel**.</span></span>

    ![Importation du package MLProducts Unity](images/AzureLabs-Lab7-44.png)

## <a name="chapter-7---checking-the-dlls-in-unity"></a><span data-ttu-id="e93b8-383">Chapitre 7-vérification des dll dans Unity</span><span class="sxs-lookup"><span data-stu-id="e93b8-383">Chapter 7 - Checking the DLLs in Unity</span></span>

<span data-ttu-id="e93b8-384">Pour tirer parti de l’utilisation de bibliothèques JSON (utilisées pour la sérialisation et la désérialisation), une DLL Newtonsoft a été implémentée avec le package que vous avez fourni.</span><span class="sxs-lookup"><span data-stu-id="e93b8-384">To leverage the use of JSON libraries (used for serializing and deserializing), a Newtonsoft DLL has been implemented with the package you brought in.</span></span> <span data-ttu-id="e93b8-385">La configuration de la bibliothèque doit être correcte, bien qu’il soit important de le vérifier (en particulier si vous rencontrez des problèmes de fonctionnement du code).</span><span class="sxs-lookup"><span data-stu-id="e93b8-385">The library should have the correct configuration, though it is worth checking (particularly if you are having issues with code not working).</span></span> 

<span data-ttu-id="e93b8-386">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="e93b8-386">To do so:</span></span>

-  <span data-ttu-id="e93b8-387">Cliquez sur le fichier Newtonsoft dans le dossier plugins et observez le panneau de l' **inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-387">Left-click on the Newtonsoft file inside the Plugins folder and look at the **Inspector panel**.</span></span> <span data-ttu-id="e93b8-388">Assurez **-vous que toutes les plateformes** sont cochées.</span><span class="sxs-lookup"><span data-stu-id="e93b8-388">Make sure **Any Platform** is ticked.</span></span> <span data-ttu-id="e93b8-389">Accédez à l' **onglet UWP** et assurez-vous que **ne pas traiter** est coché.</span><span class="sxs-lookup"><span data-stu-id="e93b8-389">Go to the **UWP tab** and also ensure **Don't process** is ticked.</span></span>

    ![Importation des dll dans Unity](images/AzureLabs-Lab7-48.png)

## <a name="chapter-8---create-the-shelfkeeper-class"></a><span data-ttu-id="e93b8-391">Chapitre 8-créer la classe ShelfKeeper</span><span class="sxs-lookup"><span data-stu-id="e93b8-391">Chapter 8 - Create the ShelfKeeper class</span></span>

<span data-ttu-id="e93b8-392">La classe **ShelfKeeper** héberge des méthodes qui contrôlent l’interface utilisateur et les produits générés dans la scène.</span><span class="sxs-lookup"><span data-stu-id="e93b8-392">The **ShelfKeeper** class hosts methods that control the UI and products spawned in the scene.</span></span>

<span data-ttu-id="e93b8-393">Dans le cadre du package importé, vous aurez reçu cette classe, bien qu’elle soit incomplète.</span><span class="sxs-lookup"><span data-stu-id="e93b8-393">As part of the imported package, you will have been given this class, though it is incomplete.</span></span> <span data-ttu-id="e93b8-394">Il est maintenant temps de terminer cette classe :</span><span class="sxs-lookup"><span data-stu-id="e93b8-394">It is now time to complete that class:</span></span>

1.  <span data-ttu-id="e93b8-395">Double-cliquez sur le script **ShelfKeeper** , dans le dossier **scripts** , pour l’ouvrir avec **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-395">Double click on the **ShelfKeeper** script, within the **Scripts** folder, to open it with **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="e93b8-396">Remplacez tout le code existant dans le script par le code suivant, qui définit la date et l’heure et a une méthode pour afficher un produit.</span><span class="sxs-lookup"><span data-stu-id="e93b8-396">Replace all the code existing in the script with the following code, which sets the time and date and has a method to show a product.</span></span>

    ```csharp
    using UnityEngine;

    public class ShelfKeeper : MonoBehaviour
    {
        /// <summary>
        /// Provides this class Singleton-like behavior
        /// </summary>
        public static ShelfKeeper instance;

        /// <summary>
        /// Unity Inspector accessible Reference to the Text Mesh object needed for data
        /// </summary>
        public TextMesh dateText;

        /// <summary>
        /// Unity Inspector accessible Reference to the Text Mesh object needed for time
        /// </summary>
        public TextMesh timeText;

        /// <summary>
        /// Provides references to the spawn locations for the products prefabs
        /// </summary>
        public Transform[] spawnPoint;

        private void Awake()
        {
            instance = this;
        }

        /// <summary>
        /// Set the text of the date in the scene
        /// </summary>
        public void SetDate(string day, string month)
        {
            dateText.text = day + " " + month;
        }

        /// <summary>
        /// Set the text of the time in the scene
        /// </summary>
        public void SetTime(string hour)
        {
            timeText.text = hour + ":00";
        }

        /// <summary>
        /// Spawn a product on the shelf by providing the name and selling grade
        /// </summary>
        /// <param name="name"></param>
        /// <param name="sellingGrade">0 being the best seller</param>
        public void SpawnProduct(string name, int sellingGrade)
        {
            Instantiate(Resources.Load(name),
                spawnPoint[sellingGrade].transform.position, spawnPoint[sellingGrade].transform.rotation);
        }
    }
    ```

3.  <span data-ttu-id="e93b8-397">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-397">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

4.  <span data-ttu-id="e93b8-398">De retour dans l’éditeur Unity, vérifiez que la classe **ShelfKeeper** ressemble à ceci :</span><span class="sxs-lookup"><span data-stu-id="e93b8-398">Back in the Unity Editor, check that the **ShelfKeeper** class looks like the below:</span></span>

    ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-51.png)

    > [!IMPORTANT]
    > <span data-ttu-id="e93b8-400">Si votre script ne possède pas les cibles de référence (par exemple, *Date (maillage de texte)* ), faites simplement glisser les objets correspondants à partir du volet de la **hiérarchie**vers les champs cibles.</span><span class="sxs-lookup"><span data-stu-id="e93b8-400">If your script does not have the reference targets (i.e. *Date (Text Mesh)*), simply drag the corresponding objects from the **Hierarchy Panel**, into the target fields.</span></span> <span data-ttu-id="e93b8-401">Voir ci-dessous pour plus d’explications, si nécessaire :</span><span class="sxs-lookup"><span data-stu-id="e93b8-401">See below for explanation, if needed:</span></span>
    > 
    > 1.  <span data-ttu-id="e93b8-402">Ouvrez le tableau de **points de génération** dans le script du composant **ShelfKeeper** en cliquant dessus avec le bouton gauche.</span><span class="sxs-lookup"><span data-stu-id="e93b8-402">Open the **Spawn Point** array within the **ShelfKeeper** component script by left-clicking it.</span></span> <span data-ttu-id="e93b8-403">Une sous-section s’affiche appelée **Size**, qui indique la taille du tableau.</span><span class="sxs-lookup"><span data-stu-id="e93b8-403">A sub-section will appear called **Size**, which indicates the size of the array.</span></span> <span data-ttu-id="e93b8-404">Tapez **3** dans la zone de texte en regard de **taille** , puis appuyez sur **entrée**, et trois emplacements seront créés sous.</span><span class="sxs-lookup"><span data-stu-id="e93b8-404">Type **3** into the textbox next to **Size** and press **Enter**, and three slots will be created beneath.</span></span>
    > 2. <span data-ttu-id="e93b8-405">Dans la **hiérarchie** , développez l’objet d’affichage de l' **heure** (en cliquant avec le bouton gauche sur la flèche à côté de lui).</span><span class="sxs-lookup"><span data-stu-id="e93b8-405">Within the **Hierarchy** expand the **Time Display** object (by left-clicking the arrow beside it).</span></span> <span data-ttu-id="e93b8-406">Ensuite, cliquez sur la ***caméra principale*** à l’intérieur de la **hiérarchie**, afin que l' **inspecteur** affiche ses informations.</span><span class="sxs-lookup"><span data-stu-id="e93b8-406">Next click the ***Main Camera*** from within the **Hierarchy**, so that the **Inspector** shows its information.</span></span>
    > 3. <span data-ttu-id="e93b8-407">Sélectionnez la **caméra principale** dans le **volet**de la hiérarchie.</span><span class="sxs-lookup"><span data-stu-id="e93b8-407">Select the **Main Camera** in the **Hierarchy Panel**.</span></span> <span data-ttu-id="e93b8-408">Faites glisser les objets **Date** et **heure** du **panneau de hiérarchie** vers les emplacements de texte de **Date** et d' **heure** dans l' **inspecteur** de la **caméra principale** dans le composant **ShelfKeeper** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-408">Drag the **Date** and **Time** objects from the **Hierarchy Panel** to the **Date Text** and **Time Text** slots within the **Inspector** of the **Main Camera** in the **ShelfKeeper** component.</span></span>
    > 4. <span data-ttu-id="e93b8-409">Faites glisser **les points de génération** à partir du panneau de la **hiérarchie** (sous l’objet *étagère* ) vers les cibles de référence d' **élément** **3** sous le tableau de **points de génération** , comme indiqué dans l’image.</span><span class="sxs-lookup"><span data-stu-id="e93b8-409">Drag the **Spawn Points** from the **Hierarchy Panel** (beneath the *Shelf* object) to the **3** **Element** reference targets beneath the **Spawn Point** array, as shown in the image.</span></span>
    > 
    >     ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-52.png)

## <a name="chapter-9---create-the-productprediction-class"></a><span data-ttu-id="e93b8-411">Chapitre 9-créer la classe ProductPrediction</span><span class="sxs-lookup"><span data-stu-id="e93b8-411">Chapter 9 - Create the ProductPrediction class</span></span>

<span data-ttu-id="e93b8-412">La classe suivante que vous allez créer est la classe **ProductPrediction** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-412">The next class you are going to create is the **ProductPrediction** class.</span></span>

<span data-ttu-id="e93b8-413">Cette classe est chargée des opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e93b8-413">This class is responsible for:</span></span>

-   <span data-ttu-id="e93b8-414">Interrogation de l’instance de **Service machine learning** , en fournissant la date et l’heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="e93b8-414">Querying the **Machine Learning Service** instance, providing the current date and time.</span></span>

-   <span data-ttu-id="e93b8-415">Désérialisation de la réponse JSON en données utilisables.</span><span class="sxs-lookup"><span data-stu-id="e93b8-415">Deserializing the JSON response into usable data.</span></span>

-   <span data-ttu-id="e93b8-416">Interprétation des données, récupération des 3 produits recommandés.</span><span class="sxs-lookup"><span data-stu-id="e93b8-416">Interpreting the data, retrieving the 3 recommended products.</span></span>

-   <span data-ttu-id="e93b8-417">Appel des méthodes de la classe **ShelfKeeper** pour afficher les données dans la scène.</span><span class="sxs-lookup"><span data-stu-id="e93b8-417">Calling the **ShelfKeeper** class methods to display the data in the Scene.</span></span>

<span data-ttu-id="e93b8-418">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="e93b8-418">To create this class:</span></span>

1.  <span data-ttu-id="e93b8-419">Accédez au dossier **scripts** , dans le **panneau Projet**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-419">Go to the **Scripts** folder, in the **Project Panel**.</span></span>

2.  <span data-ttu-id="e93b8-420">Cliquez avec le bouton droit dans le dossier, **créez** >  **C# script**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-420">Right-click inside the folder, **Create** > **C# Script**.</span></span> <span data-ttu-id="e93b8-421">Appelez le script **ProductPrediction**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-421">Call the script **ProductPrediction**.</span></span>

3.  <span data-ttu-id="e93b8-422">Double-cliquez sur le nouveau script **ProductPrediction** pour l’ouvrir avec **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-422">Double click on the new **ProductPrediction** script to open it with **Visual Studio 2017**.</span></span>

4.  <span data-ttu-id="e93b8-423">Si la boîte de dialogue **modification de fichier détectée** s’affiche, cliquez sur \***recharger la solution**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-423">If the **File Modification Detected** dialog pops up, click \***Reload Solution**.</span></span>

5.  <span data-ttu-id="e93b8-424">Ajoutez les espaces de noms suivants en haut de la classe ProductPrediction :</span><span class="sxs-lookup"><span data-stu-id="e93b8-424">Add the following namespaces to the top of the ProductPrediction class:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using System.Linq;
    using Newtonsoft.Json;
    using UnityEngine.Networking;
    using System.Runtime.Serialization;
    using System.Collections;
    ```

6.  <span data-ttu-id="e93b8-425">À l’intérieur de la classe **ProductPrediction** , insérez les deux objets suivants qui sont composés d’un certain nombre de classes imbriquées.</span><span class="sxs-lookup"><span data-stu-id="e93b8-425">Inside the **ProductPrediction** class insert the following two objects which are composed of a number of nested classes.</span></span> <span data-ttu-id="e93b8-426">Ces classes sont utilisées pour sérialiser et désérialiser le JSON pour le service Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e93b8-426">These classes are used to serialize and deserialize the JSON for the Machine Learning Service.</span></span>

    ```csharp
        /// <summary>
        /// This object represents the Prediction request
        /// It host the day of the year and hour of the day
        /// The product must be left blank when serialising
        /// </summary>
        public class RootObject
        {
            public Inputs Inputs { get; set; }
        }

        public class Inputs
        {
            public Input1 input1 { get; set; }
        }

        public class Input1
        {
            public List<string> ColumnNames { get; set; }
            public List<List<string>> Values { get; set; }
        }
    ```

    ```csharp
        /// <summary>
        /// This object containing the deserialised Prediction result
        /// It host the list of the products
        /// and the likelihood of them being sold at current date and time
        /// </summary>
        public class Prediction
        {
            public Results Results { get; set; }
        }

        public class Results
        {
            public Output1 output1;
        }

        public class Output1
        {
            public string type;
            public Value value;
        }

        public class Value
        {
            public List<string> ColumnNames { get; set; }
            public List<List<string>> Values { get; set; }
        }
    ```

7.  <span data-ttu-id="e93b8-427">Ajoutez ensuite les variables suivantes au-dessus du code précédent (afin que le code JSON soit au bas du script, sous tout le code, et à l’extérieur) :</span><span class="sxs-lookup"><span data-stu-id="e93b8-427">Then add the following variables above the previous code (so that the JSON related code is at the bottom of the script, below all other code, and out of the way):</span></span>

    ```csharp
        /// <summary>
        /// The 'Primary Key' from your Machine Learning Portal
        /// </summary>
        private string authKey = "-- Insert your service authentication key here --";

        /// <summary>
        /// The 'Request-Response' Service Endpoint from your Machine Learning Portal
        /// </summary>
        private string serviceEndpoint = "-- Insert your service endpoint here --";

        /// <summary>
        /// The Hour as set in Windows
        /// </summary>
        private string thisHour;

        /// <summary>
        /// The Day, as set in Windows
        /// </summary>
        private string thisDay;

        /// <summary>
        /// The Month, as set in Windows
        /// </summary>
        private string thisMonth;

        /// <summary>
        /// The Numeric Day from current Date Conversion
        /// </summary>
        private string dayOfTheYear;

        /// <summary>
        /// Dictionary for holding the first (or default) provided prediction 
        /// from the Machine Learning Experiment
        /// </summary>    
        private Dictionary<string, string> predictionDictionary;

        /// <summary>
        /// List for holding product prediction with name and scores
        /// </summary>
        private List<KeyValuePair<string, double>> keyValueList;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="e93b8-428">Veillez à insérer la **clé primaire** et le **point de terminaison de requête-réponse**, à partir du portail machine learning, dans les variables ici.</span><span class="sxs-lookup"><span data-stu-id="e93b8-428">Make sure to insert the **primary key** and **request-response endpoint**, from the Machine Learning Portal, into the variables here.</span></span> <span data-ttu-id="e93b8-429">Les images ci-dessous indiquent où vous avez pris la clé et le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="e93b8-429">The below images show where you would have taken the key and endpoint from.</span></span> 
    >  
    > ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-53-1.png)
    >
    > ![Machine Learning Studio : l’expérience](images/AzureLabs-Lab7-53-2.png)

8.  <span data-ttu-id="e93b8-432">Insérez ce code dans la méthode **Start ()** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-432">Insert this code within the **Start()** method.</span></span> <span data-ttu-id="e93b8-433">La méthode **Start ()** est appelée lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="e93b8-433">The **Start()** method is called when the class initializes:</span></span>

    ```csharp
        void Start()
        {
            // Call to get the current date and time as set in Windows
            GetTodayDateAndTime();

            // Call to set the HOUR in the UI
            ShelfKeeper.instance.SetTime(thisHour);

            // Call to set the DATE in the UI
            ShelfKeeper.instance.SetDate(thisDay, thisMonth);

            // Run the method to Get Predication from Azure Machine Learning
            StartCoroutine(GetPrediction(thisHour, dayOfTheYear));
        }
    ```

9.  <span data-ttu-id="e93b8-434">Voici la méthode qui collecte la date et l’heure de Windows et les convertit dans un format que notre expérience Machine Learning peut utiliser pour comparer avec les données stockées dans la table.</span><span class="sxs-lookup"><span data-stu-id="e93b8-434">The following is the method that collects the date and time from Windows and converts it into a format that our Machine Learning Experiment can use to compare with the data stored in the table.</span></span>

    ```csharp
        /// <summary>
        /// Get current date and hour
        /// </summary>
        private void GetTodayDateAndTime()
        {
            // Get today date and time
            DateTime todayDate = DateTime.Now;

            // Extrapolate the HOUR
            thisHour = todayDate.Hour.ToString();

            // Extrapolate the DATE
            thisDay = todayDate.Day.ToString();
            thisMonth = todayDate.ToString("MMM");

            // Extrapolate the day of the year
            dayOfTheYear = todayDate.DayOfYear.ToString();
        }
    ```

10. <span data-ttu-id="e93b8-435">Vous pouvez **supprimer** la méthode **Update ()** puisque cette classe ne l’utilise pas.</span><span class="sxs-lookup"><span data-stu-id="e93b8-435">You can **delete** the **Update()** method since this class will not use it.</span></span>

11. <span data-ttu-id="e93b8-436">Ajoutez la méthode suivante, qui communiquera la date et l’heure actuelles au point de terminaison Machine Learning et recevra une réponse au format JSON.</span><span class="sxs-lookup"><span data-stu-id="e93b8-436">Add the following method which will communicate the current date and time to the Machine Learning endpoint and receive a response in JSON format.</span></span>

    ```csharp
        private IEnumerator GetPrediction(string timeOfDay, string dayOfYear)
        {
            // Populate the request object 
            // Using current day of the year and hour of the day
            RootObject ro = new RootObject
            {
                Inputs = new Inputs
                {
                    input1 = new Input1
                    {
                        ColumnNames = new List<string>
                        {
                            "day",
                            "hour",
                        "product"
                        },
                        Values = new List<List<string>>()
                    }
                }
            };

            List<string> l = new List<string>
            {
                dayOfYear,
                timeOfDay,
                ""
            };

            ro.Inputs.input1.Values.Add(l);

            Debug.LogFormat("Score request built");

            // Serialise the request
            string json = JsonConvert.SerializeObject(ro);

            using (UnityWebRequest www = UnityWebRequest.Post(serviceEndpoint, "POST"))
            {
                byte[] jsonToSend = new System.Text.UTF8Encoding().GetBytes(json);
                www.uploadHandler = new UploadHandlerRaw(jsonToSend);

                www.downloadHandler = new DownloadHandlerBuffer();
                www.SetRequestHeader("Authorization", "Bearer " + authKey);
                www.SetRequestHeader("Content-Type", "application/json");
                www.SetRequestHeader("Accept", "application/json");

                yield return www.SendWebRequest();
                string response = www.downloadHandler.text;

                // Deserialize the response
                DataContractSerializer serializer;
                serializer = new DataContractSerializer(typeof(string));
                DeserialiseJsonResponse(response);
            }
        }
    ```

12. <span data-ttu-id="e93b8-437">Ajoutez la méthode suivante, qui est chargée de désérialiser la réponse JSON et de communiquer le résultat de la désérialisation à la classe **ShelfKeeper** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-437">Add the following method, which is responsible for deserializing the JSON response, and communicating the result of the deserialization to the **ShelfKeeper** class.</span></span> <span data-ttu-id="e93b8-438">Ce résultat sera le nom des trois éléments prédits pour vendre le plus à la date et à l’heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="e93b8-438">This result will be the names of the three items predicted to sell the most at current date and time.</span></span> <span data-ttu-id="e93b8-439">Insérez le code ci-dessous dans la classe **ProductPrediction** , sous la méthode précédente.</span><span class="sxs-lookup"><span data-stu-id="e93b8-439">Insert the code below into the **ProductPrediction** class, below the previous method.</span></span>

    ```csharp
        /// <summary>
        /// Deserialize the response received from the Machine Learning portal
        /// </summary>
        public void DeserialiseJsonResponse(string jsonResponse)
        {
            // Deserialize JSON
            Prediction prediction = JsonConvert.DeserializeObject<Prediction>(jsonResponse);
            predictionDictionary = new Dictionary<string, string>();

            for (int i = 0; i < prediction.Results.output1.value.ColumnNames.Count; i++)
            {
                if (prediction.Results.output1.value.Values[0][i] != null)
                {
                    predictionDictionary.Add(prediction.Results.output1.value.ColumnNames[i], prediction.Results.output1.value.Values[0][i]);
                }
            }

            keyValueList = new List<KeyValuePair<string, double>>();

            // Strip all non-results, by adding only items of interest to the scoreList
            for (int i = 0; i < predictionDictionary.Count; i++)
            {
                KeyValuePair<string, string> pair = predictionDictionary.ElementAt(i);
                if (pair.Key.StartsWith("Scored Probabilities"))
                {
                    // Parse string as double then simplify the string key so to only have the item name
                    double scorefloat = 0f;
                    double.TryParse(pair.Value, out scorefloat);
                    string simplifiedName =
                        pair.Key.Replace("\"", "").Replace("Scored Probabilities for Class", "").Trim();
                    keyValueList.Add(new KeyValuePair<string, double>(simplifiedName, scorefloat));
                }
            }

            // Sort Predictions (results will be lowest to highest)
            keyValueList.Sort((x, y) => y.Value.CompareTo(x.Value));

            // Spawn the top three items, from the keyValueList, which we have sorted
            for (int i = 0; i < 3; i++)
            {
                ShelfKeeper.instance.SpawnProduct(keyValueList[i].Key, i);
            }

            // Clear lists in case of reuse
            keyValueList.Clear();
            predictionDictionary.Clear();
        }
    ```

13. <span data-ttu-id="e93b8-440">Enregistrez **Visual Studio** et revenez à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-440">Save **Visual Studio** and head back to **Unity**.</span></span>

14. <span data-ttu-id="e93b8-441">Faites glisser le script de la classe **ProductPrediction** du dossier **script** vers l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="e93b8-441">Drag the **ProductPrediction** class script from the **Script** folder, onto the **Main Camera** object.</span></span>

15. <span data-ttu-id="e93b8-442">Enregistrez votre scène et votre **fichier** projet > **enregistrer la séquence/le fichier** > enregistrer le **projet**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-442">Save your scene and project **File** > **Save Scene/File** > **Save Project**.</span></span>

## <a name="chapter-10---build-the-uwp-solution"></a><span data-ttu-id="e93b8-443">Chapitre 10 : créer la solution UWP</span><span class="sxs-lookup"><span data-stu-id="e93b8-443">Chapter 10 - Build the UWP Solution</span></span>

<span data-ttu-id="e93b8-444">Il est maintenant temps de générer votre projet en tant que solution UWP, afin qu’il puisse s’exécuter en tant qu’application autonome.</span><span class="sxs-lookup"><span data-stu-id="e93b8-444">It is now time to build your project as a UWP solution, so that it can run as a standalone application.</span></span>

<span data-ttu-id="e93b8-445">Pour générer :</span><span class="sxs-lookup"><span data-stu-id="e93b8-445">To Build:</span></span>

1.  <span data-ttu-id="e93b8-446">Enregistrez la scène en cours en cliquant sur **fichier** > **enregistrer des scènes**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-446">Save the current scene by clicking on **File** > **Save Scenes**.</span></span>

2.  <span data-ttu-id="e93b8-447">Atteindre le **fichier** > les **paramètres de build**</span><span class="sxs-lookup"><span data-stu-id="e93b8-447">Go to **File** > **Build Settings**</span></span>

3.  <span data-ttu-id="e93b8-448">Cochez la case **projets Unity C#**  (c’est important, car cela vous permettra de modifier les classes une fois la génération terminée).</span><span class="sxs-lookup"><span data-stu-id="e93b8-448">Check the box called **Unity C# Projects** (this is important because it will allow you to edit the classes after build is completed).</span></span>

4.  <span data-ttu-id="e93b8-449">Cliquez sur **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-449">Click on **Add Open Scenes**,</span></span>

5.  <span data-ttu-id="e93b8-450">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-450">Click **Build**.</span></span>

    ![Créer la solution UWP](images/AzureLabs-Lab7-54.png)

6.  <span data-ttu-id="e93b8-452">Vous serez invité à sélectionner le dossier dans lequel vous souhaitez générer la solution.</span><span class="sxs-lookup"><span data-stu-id="e93b8-452">You will be prompted to select the folder where you want to build the Solution.</span></span>

7.  <span data-ttu-id="e93b8-453">Créez un dossier **Builds** et, dans ce dossier, créez un autre dossier avec le nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="e93b8-453">Create a **BUILDS** folder and within that folder create another folder with an appropriate name of your choice.</span></span>

8.  <span data-ttu-id="e93b8-454">Cliquez sur votre nouveau dossier, puis sur **Sélectionner un dossier**pour commencer la build à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="e93b8-454">Click your new folder and then click **Select Folder**, to begin the build at that location.</span></span>

    ![Créer la solution UWP](images/AzureLabs-Lab7-55.png)

    ![Créer la solution UWP](images/AzureLabs-Lab7-56.png)

9.  <span data-ttu-id="e93b8-457">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="e93b8-457">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-11---deploy-your-application"></a><span data-ttu-id="e93b8-458">Chapitre 11-déployer votre application</span><span class="sxs-lookup"><span data-stu-id="e93b8-458">Chapter 11 - Deploy your Application</span></span>

<span data-ttu-id="e93b8-459">Pour déployer votre application :</span><span class="sxs-lookup"><span data-stu-id="e93b8-459">To deploy your application:</span></span>

1.  <span data-ttu-id="e93b8-460">Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-460">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

2.  <span data-ttu-id="e93b8-461">Avec Visual Studio Open, vous devez restaurer les packages NuGet. pour ce faire, cliquez avec le bouton droit sur votre solution MachineLearningLab_Build, à partir de la Explorateur de solutions (à droite de Visual Studio), puis cliquez sur restaurer les packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="e93b8-461">With Visual Studio open, you need to Restore NuGet Packages, which can be done through right-clicking your MachineLearningLab_Build solution, from the Solution Explorer (found to the right of Visual Studio), and then clicking Restore NuGet Packages:</span></span>

    ![Ajouter des packages NuGet](images/AzureLabs-Lab7-57.png)

3.  <span data-ttu-id="e93b8-463">Dans la configuration de la solution, sélectionnez **Déboguer**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-463">In the Solution Configuration select **Debug**.</span></span>

4.  <span data-ttu-id="e93b8-464">Dans la plateforme de la solution, sélectionnez **x86**, **ordinateur local**.</span><span class="sxs-lookup"><span data-stu-id="e93b8-464">In the Solution Platform, select **x86**, **Local Machine**.</span></span> 

    > <span data-ttu-id="e93b8-465">Pour Microsoft HoloLens, il peut s’avérer plus facile de définir cette valeur sur *machine distante*, afin de ne pas être attaché à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e93b8-465">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="e93b8-466">Toutefois, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e93b8-466">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="e93b8-467">Identifiez l' **adresse IP** de votre HoloLens, qui se trouve dans les *paramètres > réseau & Internet > les options avancées du Wi-Fi >* ; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="e93b8-467">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="e93b8-468">Assurez-vous que le **mode développeur** est **activé**; trouvé dans *paramètres > mettre à jour & > de sécurité pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="e93b8-468">Ensure **Developer Mode** is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Ajouter des packages NuGet](images/AzureLabs-Lab7-58.png)

5.  <span data-ttu-id="e93b8-470">Accédez au **menu Générer** , puis cliquez sur **déployer la solution** pour chargement l’application sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="e93b8-470">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your PC.</span></span>

6.  <span data-ttu-id="e93b8-471">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancées.</span><span class="sxs-lookup"><span data-stu-id="e93b8-471">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

<span data-ttu-id="e93b8-472">Lorsque vous exécutez l’application de réalité mixte, vous voyez le banc qui a été configuré dans votre scène Unity et, à partir de l’initialisation, les données que vous avez configurées dans Azure sont extraites.</span><span class="sxs-lookup"><span data-stu-id="e93b8-472">When you run the Mixed Reality application, you will see the bench that was set up in your Unity scene, and from initialization, the data you set up within Azure will be fetched.</span></span> <span data-ttu-id="e93b8-473">Les données seront désérialisées au sein de votre application et les trois premiers résultats de la date et de l’heure actuelles seront fournis visuellement, sous la forme de trois modèles sur le banc d’essai.</span><span class="sxs-lookup"><span data-stu-id="e93b8-473">The data will be deserialized within your application, and the three top results for your current date and time will be provided visually, as three models on the bench.</span></span>


## <a name="your-finished-machine-learning-application"></a><span data-ttu-id="e93b8-474">Votre application Machine Learning terminée</span><span class="sxs-lookup"><span data-stu-id="e93b8-474">Your finished Machine Learning application</span></span>
 
<span data-ttu-id="e93b8-475">Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Azure Machine Learning pour effectuer des prédictions de données et les afficher sur votre scène.</span><span class="sxs-lookup"><span data-stu-id="e93b8-475">Congratulations, you built a mixed reality app that leverages the Azure Machine Learning to make data predictions and display it on your scene.</span></span>

![Ajouter des packages NuGet](images/AzureLabs-Lab7-0.png)

## <a name="exercise"></a><span data-ttu-id="e93b8-477">Exercices</span><span class="sxs-lookup"><span data-stu-id="e93b8-477">Exercise</span></span>

<span data-ttu-id="e93b8-478">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="e93b8-478">**Exercise 1**</span></span>

<span data-ttu-id="e93b8-479">Expérimentez l’ordre de tri de votre application et faites en sorte que les trois prédictions les plus basses s’affichent sur l’étagère, car ces données peuvent également être utiles.</span><span class="sxs-lookup"><span data-stu-id="e93b8-479">Experiment with the sort order of your application and have the three bottom predictions appear on the shelf, as this data would potentially be useful also.</span></span>

<span data-ttu-id="e93b8-480">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="e93b8-480">**Exercise 2**</span></span>

<span data-ttu-id="e93b8-481">L’utilisation de **tables Azure** remplit une nouvelle table avec les informations météorologiques et crée une nouvelle expérience à l’aide des données.</span><span class="sxs-lookup"><span data-stu-id="e93b8-481">Using **Azure Tables** populate a new table with weather information and create a new experiment using the data.</span></span>
