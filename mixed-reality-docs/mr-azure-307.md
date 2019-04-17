---
title: MR et Azure Machine learning 307-
description: Terminer ce cours pour apprendre à implémenter Azure Machine Learning Studio au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, apprentissage automatique, ml studio d’apprentissage machine, hololens, immersives, vr
ms.openlocfilehash: 726a6cce91d46ad878f8502381d085fb979ac72a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594338"
---
>[!NOTE]
><span data-ttu-id="8e7b0-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="8e7b0-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="8e7b0-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="8e7b0-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="8e7b0-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="8e7b0-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-307-machine-learning"></a><span data-ttu-id="8e7b0-110">MR et Azure 307 : Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8e7b0-110">MR and Azure 307: Machine learning</span></span>

![produit final-Démarrer](images/AzureLabs-Lab7-0.png)

<span data-ttu-id="8e7b0-112">Dans ce cours, vous allez apprendre à ajouter des fonctionnalités de Machine Learning (ML) à une application de réalité mixte à l’aide d’Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-112">In this course, you will learn how to add Machine Learning (ML) capabilities to a mixed reality application using Azure Machine Learning Studio.</span></span>

<span data-ttu-id="8e7b0-113">*Azure Machine Learning Studio* est un service Microsoft, qui fournit aux développeurs un grand nombre d’algorithmes d’apprentissage, ce qui peut aider à l’entrée de données, de sortie, de préparation et de visualisation.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-113">*Azure Machine Learning Studio* is a Microsoft service, which provides developers with a large number of machine learning algorithms, which can help with data input, output, preparation, and visualization.</span></span> <span data-ttu-id="8e7b0-114">À partir de ces composants, il est alors possible de développer une expérience d’analytique prédictive, effectuer une itération sur celle-ci et utilisez-la dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-114">From these components, it is then possible to develop a predictive analytics experiment, iterate on it, and use it to train your model.</span></span> <span data-ttu-id="8e7b0-115">Suivant une formation, vous pouvez rendre votre modèle opérationnel dans le cloud Azure, afin qu’il peut ensuite évaluer les nouvelles données.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-115">Following training, you can make your model operational within the Azure cloud, so that it can then score new data.</span></span> <span data-ttu-id="8e7b0-116">Pour plus d’informations, visitez le [page Azure Machine Learning Studio](https://azure.microsoft.com/en-au/services/machine-learning-studio/).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-116">For more information, visit the [Azure Machine Learning Studio page](https://azure.microsoft.com/en-au/services/machine-learning-studio/).</span></span>

<span data-ttu-id="8e7b0-117">Avoir terminé ce cours, vous disposez d’une application de casque immersives de réalité mixte et aurez appris comment effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-117">Having completed this course, you will have a mixed reality immersive headset application, and will have learned how do the following:</span></span>

1.  <span data-ttu-id="8e7b0-118">Fournir une table de données de ventes pour le *Azure Machine Learning Studio* portal et la conception un algorithme pour prédire les ventes futures d’éléments les plus courants.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-118">Provide a table of sales data to the *Azure Machine Learning Studio* portal, and        design an algorithm to predict future sales of popular items.</span></span>
2.  <span data-ttu-id="8e7b0-119">Créer un **projet Unity**, ce qui peut recevoir et interpréter les données de prédiction à partir du service de ML.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-119">Create a **Unity Project**, which can receive and interpret prediction data from the ML service.</span></span>
3.  <span data-ttu-id="8e7b0-120">Afficher les données de prédiction visuellement dans le **projet Unity**, jusqu'à fournissant des articles de la ventes les plus populaires, sur une étagère.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-120">Display the predication data visually within the **Unity Project**, through providing the most popular sales items, on a shelf.</span></span>

<span data-ttu-id="8e7b0-121">Dans votre application, il vous revient à comment vous allez intégrer les résultats avec votre conception.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-121">In your application, it is up to you as to how you will integrate the results with your design.</span></span> <span data-ttu-id="8e7b0-122">Ce cours est conçu pour vous apprendre à intégrer un Service Azure à votre projet Unity.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-122">This course is designed to teach you how to integrate an Azure Service with your Unity Project.</span></span> <span data-ttu-id="8e7b0-123">Il vous revient à utiliser les connaissances acquises à partir de ce cours pour améliorer votre application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-123">It is your job to use the knowledge you gain from this course to enhance your mixed reality application.</span></span>

<span data-ttu-id="8e7b0-124">Ce cours est un didacticiel autonome, ce qui n’implique pas directement de tous les autres laboratoires réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-124">This course is a self-contained tutorial, which does not directly involve any other Mixed Reality Labs.</span></span>

## <a name="device-support"></a><span data-ttu-id="8e7b0-125">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="8e7b0-125">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="8e7b0-126">Cours</span><span class="sxs-lookup"><span data-stu-id="8e7b0-126">Course</span></span></th><th style="width:150px"> <span data-ttu-id="8e7b0-127"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="8e7b0-127"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="8e7b0-128"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="8e7b0-128"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="8e7b0-129">MR et Azure 307 : Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8e7b0-129">MR and Azure 307: Machine learning</span></span></td><td style="text-align: center;"> <span data-ttu-id="8e7b0-130">✔️</span><span class="sxs-lookup"><span data-stu-id="8e7b0-130">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="8e7b0-131">✔️</span><span class="sxs-lookup"><span data-stu-id="8e7b0-131">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="8e7b0-132">Si ce cours se concentre principalement sur des casques Windows Mixed Reality IMMERSIFS (VR), vous pouvez également appliquer ce que vous allez apprendre dans ce cours pour Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-132">While this course primarily focuses on Windows Mixed Reality immersive (VR) headsets, you can also apply what you learn in this course to Microsoft HoloLens.</span></span> <span data-ttu-id="8e7b0-133">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-133">As you follow along with the course, you will see notes on any changes you might need to employ to support HoloLens.</span></span> <span data-ttu-id="8e7b0-134">Lorsque vous utilisez HoloLens, vous pouvez remarquer quelques echo durant la capture de la voix.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-134">When using HoloLens, you may notice some echo during voice capture.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e7b0-135">Prérequis</span><span class="sxs-lookup"><span data-stu-id="8e7b0-135">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="8e7b0-136">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-136">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="8e7b0-137">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (mai 2018).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-137">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (May 2018).</span></span> <span data-ttu-id="8e7b0-138">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer l’article outils](install-the-tools.md), mais il doit être pas supposé que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous .</span><span class="sxs-lookup"><span data-stu-id="8e7b0-138">You are free to use the latest software, as listed within the [install the tools article](install-the-tools.md), though it should not be assumed that the information in this course will perfectly match what you'll find in newer software than what's listed below.</span></span>

<span data-ttu-id="8e7b0-139">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-139">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="8e7b0-140">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="8e7b0-140">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="8e7b0-141">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="8e7b0-141">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="8e7b0-142">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="8e7b0-142">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="8e7b0-143">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="8e7b0-143">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="8e7b0-144">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8e7b0-144">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="8e7b0-145">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="8e7b0-145">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="8e7b0-146">Accès à Internet pour le programme d’installation Azure et l’extraction de données de ML</span><span class="sxs-lookup"><span data-stu-id="8e7b0-146">Internet access for Azure setup and ML data retrieval</span></span>

## <a name="before-you-start"></a><span data-ttu-id="8e7b0-147">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="8e7b0-147">Before you start</span></span>

<span data-ttu-id="8e7b0-148">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-148">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span> 

## <a name="chapter-1---azure-storage-account-setup"></a><span data-ttu-id="8e7b0-149">Chapitre 1 - Configuration d’un compte de stockage Azure</span><span class="sxs-lookup"><span data-stu-id="8e7b0-149">Chapter 1 - Azure Storage Account setup</span></span>

<span data-ttu-id="8e7b0-150">Pour utiliser l’API de Translator Azure, vous devrez configurer une instance du service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-150">To use the Azure Translator API, you will need to configure an instance of the service to be made available to your application.</span></span>
1.  <span data-ttu-id="8e7b0-151">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-151">Log in to the  [Azure Portal](https://portal.azure.com).</span></span>

    > [!NOTE]
    > <span data-ttu-id="8e7b0-152">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-152">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="8e7b0-153">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-153">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

2.  <span data-ttu-id="8e7b0-154">Une fois que vous êtes connecté, cliquez sur **comptes de stockage** dans le menu de gauche.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-154">Once you are logged in, click on **Storage Accounts** in the left menu.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-1.png)

    > [!NOTE]
    > <span data-ttu-id="8e7b0-156">Le mot **New** peut avoir été remplacé avec **créer une ressource**, dans les portails plus récente.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-156">The word **New** may have been replaced with **Create a resource**, in newer portals.</span></span>

3.  <span data-ttu-id="8e7b0-157">Sur le **comptes de stockage** onglet, cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-157">On the **Storage Accounts** tab, click on **Add**.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-2.png)

4.  <span data-ttu-id="8e7b0-159">Dans le **créer un compte de stockage** panneau :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-159">In the **Create Storage Account** panel:</span></span>

    1.  <span data-ttu-id="8e7b0-160">Insérer un **nom** pour votre compte, n’oubliez pas ce champ accepte uniquement des lettres minuscules et chiffres.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-160">Insert a **Name** for your account, be aware this field only accepts numbers, and lowercase letters.</span></span>
    2.  <span data-ttu-id="8e7b0-161">Pour **modèle de déploiement,** sélectionnez **Resource manager**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-161">For **Deployment model,** select **Resource manager**.</span></span>
    3.  <span data-ttu-id="8e7b0-162">Pour **type de compte**, sélectionnez **stockage (usage général v1)**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-162">For **Account kind**, select **Storage (general purpose v1)**.</span></span>
    4.  <span data-ttu-id="8e7b0-163">Pour **performances**, sélectionnez **Standard**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-163">For **Performance**, select **Standard**.</span></span>
    5.  <span data-ttu-id="8e7b0-164">Pour **réplication** sélectionnez **en lecture-access-geo-redundant storage (RA-GRS)**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-164">For **Replication** select **Read-access-geo-redundant storage (RA-GRS)**.</span></span>
    6.  <span data-ttu-id="8e7b0-165">Laissez **transfert sécurisé requis** comme **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-165">Leave **Secure transfer required** as **Disabled**.</span></span>
    7.  <span data-ttu-id="8e7b0-166">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-166">Select a **Subscription**.</span></span>
    4. <span data-ttu-id="8e7b0-167">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-167">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="8e7b0-168">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-168">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="8e7b0-169">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-169">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span>

        > <span data-ttu-id="8e7b0-170">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-170">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>
    
    5.  <span data-ttu-id="8e7b0-171">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-171">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="8e7b0-172">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-172">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="8e7b0-173">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-173">Some Azure assets are only available in certain regions.</span></span>

5.  <span data-ttu-id="8e7b0-174">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-174">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-3.png)

6.  <span data-ttu-id="8e7b0-176">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-176">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

7.  <span data-ttu-id="8e7b0-177">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-177">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Configuration de compte de stockage Azure](images/AzureLabs-Lab7-4.png)

## <a name="chapter-2---the-azure-machine-learning-studio"></a><span data-ttu-id="8e7b0-179">Chapitre 2 - Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="8e7b0-179">Chapter 2 - The Azure Machine Learning Studio</span></span>

<span data-ttu-id="8e7b0-180">Pour utiliser le *Azure Machine Learning*, vous devez configurer une instance du service Machine Learning à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-180">To use the *Azure Machine Learning*, you will need to configure an instance of the Machine Learning service to be made available to your application.</span></span>

1.  <span data-ttu-id="8e7b0-181">Dans le portail Azure, cliquez sur **New** dans le coin supérieur gauche coin inférieur droit, puis recherchez **espace de travail Machine Learning Studio**, appuyez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-181">In the Azure Portal, click on **New** in the top left corner, and search for **Machine Learning Studio Workspace**, press **Enter**.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-5.png)

2.  <span data-ttu-id="8e7b0-183">La nouvelle page doit fournir une description de la **espace de travail Machine Learning Studio** service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-183">The new page will provide a description of the **Machine Learning Studio Workspace**  service.</span></span> <span data-ttu-id="8e7b0-184">En bas à gauche de cette invite, cliquez sur le **créer** bouton permettant de créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-184">At the bottom left of this prompt, click the **Create** button, to create an association with this service.</span></span>

3.  <span data-ttu-id="8e7b0-185">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche où vous devez fournir des détails sur votre nouvelle **service Machine Learning Studio**:</span><span class="sxs-lookup"><span data-stu-id="8e7b0-185">Once you have clicked on **Create**, a panel will appear where you need to provide some details about your new **Machine Learning Studio service**:</span></span>

    1.  <span data-ttu-id="8e7b0-186">Insérez votre souhaitée **nom de l’espace de travail** pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-186">Insert your desired **Workspace name** for this service instance.</span></span>

    2.  <span data-ttu-id="8e7b0-187">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-187">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="8e7b0-188">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-188">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="8e7b0-189">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-189">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="8e7b0-190">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces laboratoires) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-190">It is recommended to keep all the Azure services associated with a single project (e.g. such as these labs) under a common resource group).</span></span> 

        > <span data-ttu-id="8e7b0-191">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-191">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    4.  <span data-ttu-id="8e7b0-192">Déterminer le **emplacement** pour votre groupe de ressources (si vous créez un nouveau groupe de ressources).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-192">Determine the **Location** for your resource group (if you are creating a new Resource Group).</span></span> <span data-ttu-id="8e7b0-193">Dans l’idéal, l’emplacement serait dans la région où l’application s’exécute.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-193">The location would ideally be in the region where the application would run.</span></span> <span data-ttu-id="8e7b0-194">Certaines ressources Azure sont uniquement disponibles dans certaines régions.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-194">Some Azure assets are only available in certain regions.</span></span> <span data-ttu-id="8e7b0-195">Vous devez utiliser le même groupe de ressources que vous avez utilisé pour créer le stockage Azure dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-195">You should use the same resource group that you used for creating the Azure Storage in the previous Chapter.</span></span>

    5.  <span data-ttu-id="8e7b0-196">Pour le **compte de stockage** , cliquez sur **utiliser l’existant**, puis cliquez sur le menu déroulant, puis à partir de là, cliquez sur le **compte de stockage** vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-196">For the **Storage account** section, click **Use existing**, then click the dropdown menu, and from there, click the **Storage Account** you created in the last Chapter.</span></span>

    6.  <span data-ttu-id="8e7b0-197">Sélectionnez l’option appropriée **espace de travail de niveau tarifaire** pour vous, dans le menu déroulant.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-197">Select the appropriate **Workspace pricing tier** for you, from the dropdown menu.</span></span>

    7.  <span data-ttu-id="8e7b0-198">Dans le **plan de service Web** , cliquez sur **créer** **nouveau,** puis insérez un nom pour celle-ci dans le champ de texte.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-198">Within the **Web service plan** section, click **Create** **new,** then insert a name for it in the text field.</span></span>

    8.  <span data-ttu-id="8e7b0-199">À partir de la **niveau tarifaire du plan de service Web** , sélectionnez le niveau de prix de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-199">From the **Web service plan pricing tier** section, select the price tier of your choice.</span></span> <span data-ttu-id="8e7b0-200">Un environnement de développement test niveau appelé **DEVTEST Standard** doivent être disponibles pour vous sans frais.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-200">A development testing tier called **DEVTEST Standard** should be available to you at no charge.</span></span>

    9.  <span data-ttu-id="8e7b0-201">Vous devez également confirmer que vous avez compris les termes et Conditions appliquées à ce Service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-201">You will also need to confirm that you have understood the Terms and Conditions applied to this Service.</span></span>

    10. <span data-ttu-id="8e7b0-202">Cliquez sur **Create (Créer)**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-202">Click **Create**.</span></span>

        ![Azure Machine Learning Studio](images/AzureLabs-Lab7-6.png)

4.  <span data-ttu-id="8e7b0-204">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-204">Once you have clicked on **Create**, you will have to wait for the service to be created, this might take a minute.</span></span>

5.  <span data-ttu-id="8e7b0-205">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-205">A notification will appear in the portal once the Service instance is created.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-7.png)

6.  <span data-ttu-id="8e7b0-207">Cliquez sur la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-207">Click on the notification to explore your new Service instance.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-8.png)

7.  <span data-ttu-id="8e7b0-209">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-209">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span>

8.  <span data-ttu-id="8e7b0-210">Dans la page affichée sous la **liens supplémentaires** , cliquez sur **lancer Machine Learning Studio**, qui sera votre navigateur, à la **Machine Learning Studio** portail.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-210">In the page displayed, under the **Additional Links** section, click **Launch Machine Learning Studio**, which will direct your browser to the **Machine Learning Studio** portal.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-9.png)

9.  <span data-ttu-id="8e7b0-212">Utilisez le **Sign In** button, en haut à droite ou dans le centre de se connecter à votre Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-212">Use the **Sign In** button, at the top right or in the center, to log into your Machine Learning Studio.</span></span>

    ![Azure Machine Learning Studio](images/AzureLabs-Lab7-10.png)


## <a name="chapter-3---the-machine-learning-studio-dataset-setup"></a><span data-ttu-id="8e7b0-214">Chapitre 3 - Machine Learning Studio : Programme d’installation de jeu de données</span><span class="sxs-lookup"><span data-stu-id="8e7b0-214">Chapter 3 - The Machine Learning Studio: Dataset setup</span></span>

<span data-ttu-id="8e7b0-215">Une des manières d’utiliser des algorithmes d’apprentissage automatique en analysant les données existantes et puis tente de prédire les futurs résultats repose sur le jeu de données existant.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-215">One of the ways Machine Learning algorithms work is by analyzing existing data and then attempting to predict future results based on the existing data set.</span></span> <span data-ttu-id="8e7b0-216">Ce qui signifie généralement les données plus existantes que vous avez, plus l’algorithme sera à prédire les futurs résultats.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-216">This generally means that the more existing data you have, the better the algorithm will be at predicting future results.</span></span>

<span data-ttu-id="8e7b0-217">Un exemple de table vous est fourni, ce cours, appelé [ProductsTableCSV et peut être téléchargé ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-217">A sample table is provided to you, for this course, called [ProductsTableCSV and can be downloaded here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/MR%20and%20Azure%20307%20-%20Machine%20learning.zip).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e7b0-218">Le fichier .zip ci-dessus contient à la fois le **ProductsTableCSV** et **.unitypackage**, dont vous aurez besoin dans [chapitre 6](#chapter-6---importing-the-mlproducts-unity-package).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-218">The above .zip file contains both the **ProductsTableCSV** and the **.unitypackage**, which you will need in [Chapter 6](#chapter-6---importing-the-mlproducts-unity-package).</span></span> <span data-ttu-id="8e7b0-219">Ce package est également fourni dans ce chapitre, bien que distinct dans le fichier csv.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-219">This package is also provided within that Chapter, though separate to the csv file.</span></span>

<span data-ttu-id="8e7b0-220">Ce jeu de données exemple contient un enregistrement des objets pape de toutes les heures de chaque jour de l’année 2017.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-220">This sample data set contains a record of the best-selling objects at every hour of each day of the year 2017.</span></span>
        
![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-11.png)

<span data-ttu-id="8e7b0-222">Par exemple, le jour 1 de 2017, à 13 h 00 (heure 13), l’élément pape était salt et poivre.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-222">For example, on day 1 of 2017, at 1pm (hour 13), the best-selling item was salt and pepper.</span></span>

<span data-ttu-id="8e7b0-223">Cet exemple de table contient des 9998 entrées.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-223">This sample table contains 9998 entries.</span></span>

1.  <span data-ttu-id="8e7b0-224">Revenez à la **Machine Learning Studio** portail, et ajoutez cette table comme un **Dataset** pour votre ML.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-224">Head back to the **Machine Learning Studio** portal, and add this table as a **Dataset** for your ML.</span></span> <span data-ttu-id="8e7b0-225">Cela en cliquant sur le **+ nouveau** bouton dans le coin inférieur gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-225">Do this by clicking the **+ New** button in the bottom left corner of the screen.</span></span>

    ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-12.png)

2.  <span data-ttu-id="8e7b0-227">Une section s’allumera à partir du bas et au sein qu’il existe le panneau de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-227">A section will come up from the bottom, and within that there is navigation panel on the left.</span></span> <span data-ttu-id="8e7b0-228">Cliquez sur **Dataset**, puis vers la droite, **à partir d’un fichier Local**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-228">Click **Dataset**, then to the right of that, **From Local File**.</span></span>

    ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-13.png)

3.  <span data-ttu-id="8e7b0-230">Charger le nouveau **Dataset** en suivant ces étapes :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-230">Upload the new **Dataset** by following these steps:</span></span>

    1. <span data-ttu-id="8e7b0-231">La fenêtre de chargement s’affiche, dans laquelle vous pouvez **Parcourir** votre disque dur pour le nouveau jeu de données.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-231">The upload window will appear, where you can **Browse** your hard drive for the new dataset.</span></span>

        ![Machine Learning Studio : Programme d’installation de jeu de données](images/AzureLabs-Lab7-14.png)

    2.  <span data-ttu-id="8e7b0-233">Une fois la sélection et dans la fenêtre de chargement, laissez la case à cocher décoché.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-233">Once selected, and back in the upload window, leave the checkbox unticked.</span></span>

    3.  <span data-ttu-id="8e7b0-234">Dans le champ de texte ci-dessous, entrez **ProductsTableCSV.csv** comme nom pour le jeu de données (bien que doit être ajouté automatiquement).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-234">In the text field below, enter **ProductsTableCSV.csv** as the name for the dataset (though should automatically be added).</span></span>

    4.  <span data-ttu-id="8e7b0-235">À l’aide de la liste déroulante pour **Type**, sélectionnez **fichier CSV générique avec un en-tête (.csv)**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-235">Using the dropdown menu for **Type**, select **Generic CSV File with a header (.csv)**.</span></span>

    5.  <span data-ttu-id="8e7b0-236">Appuyez sur les graduations dans la partie inférieure droite de la fenêtre de chargement et votre **Dataset** sera téléchargé.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-236">Press the tick in the bottom right of the upload window, and your **Dataset** will be uploaded.</span></span>

## <a name="chapter-4---the-machine-learning-studio-the-experiment"></a><span data-ttu-id="8e7b0-237">Chapitre 4 - Machine Learning Studio : L’expérience</span><span class="sxs-lookup"><span data-stu-id="8e7b0-237">Chapter 4 - The Machine Learning Studio: The Experiment</span></span>

<span data-ttu-id="8e7b0-238">Avant de pouvoir générer votre système d’apprentissage automatique, vous devez créer une expérience, pour valider votre théorie sur vos données.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-238">Before you can build your machine learning system, you will need to build an experiment, to validate your theory about your data.</span></span> <span data-ttu-id="8e7b0-239">Avec les résultats, vous savez que vous ayez besoin de davantage de données, ou s’il n’existe aucune corrélation entre les données et un résultat possible.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-239">With the results, you will know whether you need more data, or if there is no correlation between the data and a possible outcome.</span></span>

<span data-ttu-id="8e7b0-240">Pour commencer à créer une expérience :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-240">To start creating an experiment:</span></span>

1.  <span data-ttu-id="8e7b0-241">Cliquez de nouveau sur le **+ nouveau** bouton dans la coin inférieur gauche de la page, puis cliquez sur **expérience** > **expérience vide**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-241">Click again on the **+ New** button on the bottom left of the page, then click on **Experiment** > **Blank Experiment**.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-15.png)

2.  <span data-ttu-id="8e7b0-243">Une nouvelle page s’affiche avec une expérience vide :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-243">A new page will be displayed with a blank Experiment:</span></span>

3.  <span data-ttu-id="8e7b0-244">À partir du panneau sur la gauche développer \**jeux de données enregistrés* > \* Mes jeux de données \*\* et faites glisser le **ProductsTableCSV** à la **canevas de l’expérience**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-244">From the panel on the left expand \**Saved Datasets* > \*My Datasets\*\* and drag the  **ProductsTableCSV** on to the **Experiment Canvas**.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-16.png)

4.  <span data-ttu-id="8e7b0-246">Dans le volet gauche, développez **Transformation des données** > **Sample and Split**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-246">In the panel on the left, expand **Data Transformation** > **Sample and Split**.</span></span> <span data-ttu-id="8e7b0-247">Puis faites glisser le **fractionner les données** élément dans le **canevas de l’expérience**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-247">Then drag the **Split Data** item in to the **Experiment Canvas**.</span></span> <span data-ttu-id="8e7b0-248">L’élément de données de fractionnement fractionne le jeu de données en deux parties.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-248">The Split Data item will split the data set into two parts.</span></span> <span data-ttu-id="8e7b0-249">Une partie, vous allez utiliser pour l’apprentissage de l’algorithme d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-249">One part you will use for training the machine learning algorithm.</span></span> <span data-ttu-id="8e7b0-250">La deuxième partie est utilisée pour évaluer la précision de l’algorithme généré.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-250">The second part will be used to evaluate the accuracy of the algorithm generated.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-17.png)

5.  <span data-ttu-id="8e7b0-252">Dans le volet de droite (lors de la fractionner les données élément sur le canevas est sélectionné), modifiez le **Fraction de lignes dans le premier jeu de données de sortie** à **0,7**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-252">In the right panel (while the Split Data item on the canvas is selected), edit the **Fraction of rows in the first output dataset** to **0.7**.</span></span> <span data-ttu-id="8e7b0-253">Il fractionne les données en deux parties, la première partie sera 70 % des données, et la deuxième partie est le 30 % restantes.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-253">This will split the data into two parts, the first part will be 70% of the data, and the second part will be the remaining 30%.</span></span> <span data-ttu-id="8e7b0-254">Pour garantir que les données sont fractionnées de façon aléatoire, vérifiez que le **fractionnement aléatoire** case à cocher reste cochée.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-254">To ensure that the data is split randomly, make sure the **Randomized split** checkbox remains checked.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-18.png)

6.  <span data-ttu-id="8e7b0-256">Faites glisser une connexion à partir de la base de la **ProductsTableCSV** élément sur le canevas en haut de l’élément de fractionner les données.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-256">Drag a connection from the base of the **ProductsTableCSV** item on the canvas to the top of the Split Data item.</span></span> <span data-ttu-id="8e7b0-257">Cela lier des éléments et envoyer le **ProductsTableCSV** sortie du jeu de données (données) à fractionner les données d’entrée.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-257">This will connect the items and send the **ProductsTableCSV** dataset output (the data) to the Split Data input.</span></span>  

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-19.png)

7.  <span data-ttu-id="8e7b0-259">Dans le **expériences** panneau sur le côté gauche, développez \**Machine Learning* > \* Train **. Faites glisser le **former modèle \*\* élément out dans la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-259">In the **Experiments** panel on the left side, expand \**Machine Learning* > \*Train **. Drag the **Train Model\*\* item out in to the Experiment canvas.</span></span> <span data-ttu-id="8e7b0-260">La zone de travail doit se présenter le même que le ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-260">Your canvas should look the same as the below.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-20.png)

8.  <span data-ttu-id="8e7b0-262">À partir de la ***en bas à gauche*** de la **fractionner les données** élément faites glisser une connexion à la **en haut à droite** de la **former le modèle** élément.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-262">From the ***bottom left*** of the **Split Data** item drag a connection to the **top right** of the **Train Model** item.</span></span> <span data-ttu-id="8e7b0-263">La première division de 70 % du jeu de données se servira pour l’apprentissage de l’algorithme de former le modèle.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-263">The first 70% split from the dataset will be used by the Train Model to train the algorithm.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-21.png)

9.  <span data-ttu-id="8e7b0-265">Sélectionnez le **former le modèle** élément sur le canevas et, dans le **propriétés** cliquez sur Panneau de configuration (sur le côté droit de la fenêtre du navigateur) le **lancer le sélecteur de colonne**  bouton.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-265">Select the **Train Model** item on the canvas, and in the **Properties** panel (on the right-hand side of your browser window) click the **Launch column selector** button.</span></span>

10. <span data-ttu-id="8e7b0-266">Dans le type de zone de texte **produit** , puis appuyez sur **entrée**, *produit* sera définie comme une colonne pour l’apprentissage des prédictions.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-266">In the text box type **product** and then press **Enter**, *product* will be set as a column to train predictions.</span></span> <span data-ttu-id="8e7b0-267">Ensuite, cliquez sur le **graduation** en bas à droite pour fermer la boîte de dialogue de sélection.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-267">Following this, click on the **tick** in the bottom-right corner to close the selection dialog.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-22.png)

11. <span data-ttu-id="8e7b0-269">Vous vous apprêtez à former un **Multiclass Logistic Regression** algorithme pour prédire les plus vendus **produit** selon l’heure de la journée et la date.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-269">You are going to train a **Multiclass Logistic Regression** algorithm to predict the most sold **product** based on the hour of the day and the date.</span></span> <span data-ttu-id="8e7b0-270">Il n’entre pas dans le cadre de ce document pour expliquer les détails des différents algorithmes fournis par Azure Machine Learning studio, cependant, vous pouvez trouver plus d’informations à partir de la [Machine Learning aide-mémoire d’algorithme](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)</span><span class="sxs-lookup"><span data-stu-id="8e7b0-270">It is beyond the scope of this document to explain the details of the different algorithms provided by the Azure Machine Learning studio, though, you can find out more from the [Machine Learning Algorithm Cheat Sheet](https://docs.microsoft.com/azure/machine-learning/studio/algorithm-cheat-sheet)</span></span>

12. <span data-ttu-id="8e7b0-271">Dans le panneau éléments expérience sur la gauche, développez \*\**Machine Learning* > *initialiser le modèle* > \* classement \***et faites glisser le **Multiclass Logistique régression \*\* élément une session sur le canevas d’expérience.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-271">From the experiment items panel on the left, expand \*\**Machine Learning* > *Initialize Model* > \*Classification\***, and drag the **Multiclass Logistic Regression\*\* item on to the experiment canvas.</span></span>

13. <span data-ttu-id="8e7b0-272">Connectez la sortie, en bas de la **Multiclass Logistic Regression**, à l’entrée de l’angle supérieur gauche de la **former le modèle** élément.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-272">Connect the output, from the bottom of the **Multiclass Logistic Regression**, to the top-left input of the **Train Model** item.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-23.png)

14. <span data-ttu-id="8e7b0-274">Dans la liste des éléments d’expérience dans le volet gauche, développez \**Machine Learning* > \* Score**et faites glisser le **élément de modèle de Score \*\* une session sur le canevas.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-274">In list of experiment items in the panel on the left, expand \**Machine Learning* > \*Score **, and drag the **Score Model\*\* item on to the canvas.</span></span>

15. <span data-ttu-id="8e7b0-275">Connectez la sortie, en bas de la **former le modèle**, à l’entrée de l’angle supérieur gauche de la **noter le modèle**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-275">Connect the output, from the bottom of the **Train Model**, to the top-left input of the **Score Model**.</span></span>

16. <span data-ttu-id="8e7b0-276">Connectez la sortie en bas à droite de **fractionner les données**, à l’entrée en haut à droite de la \**noter le modèle* élément \*.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-276">Connect the bottom-right output from **Split Data**, to the top-right input of the \**Score Model* item\*.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-24.png)

17. <span data-ttu-id="8e7b0-278">Dans la liste des **expérience** éléments dans le volet gauche, développez \*\**Machine Learning* > \* évaluer \***et faites glisser le **élément modèle \*\* évaluer sur le canevas.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-278">In the list of **Experiment** items in the panel on the left, expand \*\**Machine Learning* > \*Evaluate\***, and drag the **Evaluate Model\*\* item onto the canvas.</span></span>

18. <span data-ttu-id="8e7b0-279">Connectez la sortie à partir de la **noter le modèle** à l’entrée de l’angle supérieur gauche de la **évaluer le modèle**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-279">Connect the output from the **Score Model** to the top-left input of the **Evaluate Model**.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-25.png)

19. <span data-ttu-id="8e7b0-281">Vous avez créé votre première expérience d’apprentissage Machine.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-281">You have built your first Machine Learning Experiment.</span></span> <span data-ttu-id="8e7b0-282">Vous pouvez maintenant enregistrer et exécuter l’expérience.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-282">You can now save and run the experiment.</span></span> <span data-ttu-id="8e7b0-283">Dans le menu en bas de la page, cliquez sur le **enregistrer** bouton pour enregistrer votre expérience, puis sur **exécuter** au début de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-283">In the menu at the bottom of the page, click on the **Save** button to save your experiment and then click **Run** to the start the experiment.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-26.png)

20. <span data-ttu-id="8e7b0-285">Vous pouvez voir le **état** de l’expérience dans l’angle supérieur droit de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-285">You can see the **status** of the experiment in the top-right of the canvas.</span></span> <span data-ttu-id="8e7b0-286">Attendez quelques instants pour l’expérience se termine.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-286">Wait a few moments for the experiment to finish.</span></span>

    > <span data-ttu-id="8e7b0-287">Si vous avez un jeu de données volumineuses (réel), il est probable que l’expérience peut prendre des heures à exécuter.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-287">If you have a big (real world) dataset it is likely that the experiment could take hours to run.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-27.png)

21. <span data-ttu-id="8e7b0-289">Cliquez avec le bouton droit sur le **évaluer le modèle** d’élément dans la zone de dessin et le pointage de menu contextuel à partir de la souris sur **résultats d’évaluation**, puis sélectionnez **visualiser**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-289">Right click on the **Evaluate Model** item in the canvas and from the context menu hover the mouse over **Evaluation Results**, then select **Visualize**.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-28.png)

22. <span data-ttu-id="8e7b0-291">Les résultats d’évaluation seront affiche en montrant les résultats prédits par rapport aux résultats réels.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-291">The evaluation results will be displayed showing the predicted outcomes versus the actual outcomes.</span></span> <span data-ttu-id="8e7b0-292">Cet exemple utilise le 30 % du dataset d’origine, qui a été fractionné précédemment, pour évaluer le modèle.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-292">This uses the 30% of the original dataset, that was split earlier, for evaluating the model.</span></span> <span data-ttu-id="8e7b0-293">Vous pouvez voir que les résultats ne sont pas très bien, dans l’idéal, vous aurez le plus grand nombre dans chaque ligne est l’élément en surbrillance dans les colonnes.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-293">You can see the results are not great, ideally you would have the highest number in each row be the highlighted item in the columns.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-29.png)

23. <span data-ttu-id="8e7b0-295">Fermer le **résultats**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-295">Close the **Results**.</span></span>

24. <span data-ttu-id="8e7b0-296">Pour utiliser votre modèle Machine Learning reformé, vous devez exposer en tant qu’un **Service Web**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-296">To use your newly trained Machine Learning model you need to expose it as a **Web Service**.</span></span> <span data-ttu-id="8e7b0-297">Pour ce faire, cliquez sur le **configurer le Service Web** dans le menu en bas de la page d’élément de menu, puis cliquez sur **Service Web prédictif**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-297">To do this, click on the **Set Up Web Service** menu item in the menu at the bottom of the page, and click on **Predictive Web Service**.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-30.png)

25. <span data-ttu-id="8e7b0-299">Un nouvel onglet est créé, et le former le modèle fusionnés pour créer le nouveau service web.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-299">A new tab will be created, and the train model merged to create the new web service.</span></span> 

26. <span data-ttu-id="8e7b0-300">Dans le menu en bas de la page, cliquez sur **enregistrer**, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-300">In the menu at the bottom of the page click **Save**, then click **Run**.</span></span><span data-ttu-id="8e7b0-301"> Vous verrez l’état mis à jour dans l’angle supérieur droit de la zone de dessin.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-301"> You will see the status updated in the top-right corner of the experiment canvas.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-31.png)

27. <span data-ttu-id="8e7b0-303">Une fois qu’elle est terminée, un **déployer le Service Web** bouton s’affiche en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-303">Once it has finished running, a **Deploy Web Service** button will appear at the bottom of the page.</span></span> <span data-ttu-id="8e7b0-304">Vous êtes prêt à déployer le service web.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-304">You are ready to deploy the web service.</span></span> <span data-ttu-id="8e7b0-305">Cliquez sur **déployer le Service Web** (classique) dans le menu en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-305">Click **Deploy Web Service** (Classic) in the menu at the bottom of the page.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-32.png)

    > <span data-ttu-id="8e7b0-307">Votre navigateur peut vous demander pour autoriser une fenêtre contextuelle, ce qui vous convient **autoriser**, bien que vous devrez peut-être appuyer sur **déployer le Service Web** là encore, si la page déployer n’apparaît pas.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-307">Your browser may prompt to allow a pop-up, which you should **allow**, though you may need to press **Deploy Web Service** again, if the deploy page does not show.</span></span> 

28. <span data-ttu-id="8e7b0-308">Une fois que l’expérience a été créée, vous serez redirigé vers un **tableau de bord** page où vous disposerez votre **clé API** affiché.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-308">Once the Experiment has been created you will be redirected to a **Dashboard** page where you will have your **API Key** displayed.</span></span> <span data-ttu-id="8e7b0-309">Copier dans un bloc-notes pour le moment, vous en aurez besoin très bientôt dans votre code.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-309">Copy it into a notepad for the moment, you will need it in your code very soon.</span></span> <span data-ttu-id="8e7b0-310">Une fois que vous avez indiqué votre clé API, cliquez sur le **demande/réponse** situé dans le **le point de terminaison par défaut** section en dessous de la clé.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-310">Once you have noted your API Key, click on the **REQUEST/RESPONSE** button in the **Default Endpoint** section underneath the Key.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-33.png)

    > [!NOTE] 
    > <span data-ttu-id="8e7b0-312">Si vous cliquez sur Test dans cette page, vous serez en mesure d’entrer des données d’entrée et afficher la sortie.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-312">If you click Test in this page, you will be able to enter input data and view the output.</span></span> <span data-ttu-id="8e7b0-313">Entrez le **jour** et **heure**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-313">Enter the **day** and **hour**.</span></span> <span data-ttu-id="8e7b0-314">Laissez le **produit** entrée vide.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-314">Leave the **product** entry blank.</span></span> <span data-ttu-id="8e7b0-315">Puis cliquez sur le **confirmer** bouton.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-315">Then click the **Confirm** button.</span></span><span data-ttu-id="8e7b0-316"> La sortie au bas de la page affiche l’objet JSON qui représente la probabilité de chaque produit qui est le choix.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-316"> The output on the bottom of the page will show the JSON representing the likelihood of each product being the choice.</span></span>

29. <span data-ttu-id="8e7b0-317">Une nouvelle page web s’ouvre, affichant les instructions et des exemples sur la structure de requête requis par Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-317">A new web page will open up, displaying the instructions and some examples about the Request structure required by the Machine Learning Studio.</span></span> <span data-ttu-id="8e7b0-318">Copie le **URI de requête** affichés dans cette page, dans votre bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-318">Copy the **Request URI** displayed in this page, into your notepad.</span></span>

    ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-34.png)

<span data-ttu-id="8e7b0-320">Vous avez maintenant créé un système de machine learning qui fournit le produit plus susceptible d’être vendus en fonction des données historiques d’achat, mis en corrélation avec l’heure de la journée et le jour de l’année.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-320">You have now built a machine learning system that provides the most likely product to be sold based on historical purchasing data, correlated with the time of the day and day of the year.</span></span>

<span data-ttu-id="8e7b0-321">Pour appeler le service web, vous devez l’URL pour le point de terminaison de service et une clé d’API pour le service.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-321">To call the web service, you will need the URL for the service endpoint and an API Key for the service.</span></span> <span data-ttu-id="8e7b0-322">Cliquez sur le **consommer** onglet, dans le menu supérieur.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-322">Click on the **Consume** tab, from the top menu.</span></span>

<span data-ttu-id="8e7b0-323">Le **consommation** page d’informations affiche les informations que vous devez appeler le service web à partir de votre code.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-323">The **Consumption** Info page will display the information you will need to call the web service from your code.</span></span> <span data-ttu-id="8e7b0-324">Effectuez une copie de la **clé primaire** et le **demande-réponse** URL.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-324">Take a copy of the **Primary Key** and the **Request-Response** URL.</span></span> <span data-ttu-id="8e7b0-325">Vous en aurez besoin dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-325">You will need these in the next Chapter.</span></span>

## <a name="chapter-5---setting-up-the-unity-project"></a><span data-ttu-id="8e7b0-326">Chapitre 5 : configuration du projet Unity</span><span class="sxs-lookup"><span data-stu-id="8e7b0-326">Chapter 5 - Setting up the Unity Project</span></span>

<span data-ttu-id="8e7b0-327">Configurer et tester votre casque immersives de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-327">Set up and test your Mixed Reality Immersive Headset.</span></span>

> [!NOTE]
>  <span data-ttu-id="8e7b0-328">Vous allez **pas** nécessitent des contrôleurs de mouvement pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-328">You will **not** require Motion Controllers for this course.</span></span> <span data-ttu-id="8e7b0-329">Si vous avez besoin de prendre en charge de paramétrage le casque immersives, veuillez cliquer [ici](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-329">If you need support setting up the Immersive Headset, please click [HERE](https://support.microsoft.com/en-au/help/4043101/windows-10-set-up-windows-mixed-reality).</span></span>

1.  <span data-ttu-id="8e7b0-330">Ouvrez **Unity** et créez un projet Unity appelé **MR\_MachineLearning.**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-330">Open **Unity** and create a new Unity Project called **MR\_MachineLearning.**</span></span> <span data-ttu-id="8e7b0-331">Assurez-vous que le type de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-331">Make sure the project type is set to **3D**.</span></span>

2.  <span data-ttu-id="8e7b0-332">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-332">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="8e7b0-333">Accédez à ***modifier* > *préférences*** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-333">Go to ***Edit* > *Preferences*** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="8e7b0-334">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-334">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="8e7b0-335">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-335">Close the **Preferences** window.</span></span>

3.  <span data-ttu-id="8e7b0-336">Ensuite, accédez à ***fichier* > *paramètres de Build*** et basculer de la plateforme à **plateforme Windows universelle**, en cliquant sur le ***plateforme de commutation*** bouton.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-336">Next, go to ***File* > *Build Settings*** and switch the platform to **Universal Windows Platform**, by clicking on the ***Switch Platform*** button.</span></span>

4.  <span data-ttu-id="8e7b0-337">Assurez-vous également que :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-337">Also make sure that:</span></span>

    1.  <span data-ttu-id="8e7b0-338">**Équipement cible** a la valeur **n’importe quel appareil**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-338">**Target Device** is set to **Any Device**.</span></span>

        > <span data-ttu-id="8e7b0-339">Pour le Microsoft HoloLens, définissez **appareil cible** à *HoloLens*.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-339">For the Microsoft HoloLens, set **Target Device** to *HoloLens*.</span></span>

    2.  <span data-ttu-id="8e7b0-340">**Type de build** a la valeur **D3D**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-340">**Build Type** is set to **D3D**.</span></span>

    3.  <span data-ttu-id="8e7b0-341">**Kit de développement logiciel** a la valeur **dernière installé**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-341">**SDK** is set to **Latest installed**.</span></span>

    4.  <span data-ttu-id="8e7b0-342">**Version de Visual Studio** a la valeur **dernière installé**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-342">**Visual Studio Version** is set to **Latest installed**.</span></span>

    5.  <span data-ttu-id="8e7b0-343">**Générez et exécutez** a la valeur **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-343">**Build and Run** is set to **Local Machine**.</span></span>

    6.  <span data-ttu-id="8e7b0-344">Ne vous inquiétez pas sur la configuration de **scènes** dès que ces éléments sont fournis plus loin.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-344">Do not worry about setting up **Scenes** right now, as these are provided later.</span></span>

    7.  <span data-ttu-id="8e7b0-345">Les autres paramètres doivent être conservées comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-345">The remaining settings should be left as default for now.</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab7-35.png)

5.  <span data-ttu-id="8e7b0-347">Dans le **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-347">In the **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span> 

6. <span data-ttu-id="8e7b0-348">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-348">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="8e7b0-349">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-349">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="8e7b0-350">**Écriture de scripts** **Version du Runtime** doit être **expérimental** (équivalent .NET 4.6)</span><span class="sxs-lookup"><span data-stu-id="8e7b0-350">**Scripting** **Runtime Version** should be **Experimental** (.NET 4.6 Equivalent)</span></span>

        2. <span data-ttu-id="8e7b0-351">**Script principal** doit être ***.NET***</span><span class="sxs-lookup"><span data-stu-id="8e7b0-351">**Scripting Backend** should be ***.NET***</span></span>

        3. <span data-ttu-id="8e7b0-352">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-352">**API Compatibility Level** should be **.NET 4.6**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab7-36.png)

    2.  <span data-ttu-id="8e7b0-354">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-354">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        - <span data-ttu-id="8e7b0-355">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-355">**InternetClient**</span></span>

            ![Configuration du projet Unity](images/AzureLabs-Lab7-37.png)

    3.  <span data-ttu-id="8e7b0-357">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté</span><span class="sxs-lookup"><span data-stu-id="8e7b0-357">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added</span></span>

        ![Configuration du projet Unity](images/AzureLabs-Lab7-38.png)

    

6.  <span data-ttu-id="8e7b0-359">Dans **paramètres de Build** *Unity C#*  projets est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-359">Back in **Build Settings** *Unity C#* Projects is no longer greyed out; tick the checkbox next to this.</span></span> 

7.  <span data-ttu-id="8e7b0-360">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-360">Close the Build Settings window.</span></span>

8.  <span data-ttu-id="8e7b0-361">Enregistrer votre projet (**fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-361">Save your Project (**FILE > SAVE PROJECT**).</span></span>

## <a name="chapter-6---importing-the-mlproducts-unity-package"></a><span data-ttu-id="8e7b0-362">Chapitre 6 - importation du Package MLProducts Unity</span><span class="sxs-lookup"><span data-stu-id="8e7b0-362">Chapter 6 - Importing the MLProducts Unity Package</span></span>

<span data-ttu-id="8e7b0-363">Pour ce cours, vous devez télécharger un Package de ressource Unity appelé [ **Azure-MR-307.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-363">For this course, you will need to download a Unity Asset Package called [**Azure-MR-307.unitypackage**](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20307%20-%20Machine%20learning/307-Scene-Setup.unitypackage).</span></span> <span data-ttu-id="8e7b0-364">Ce package est livrée avec une scène, tous les objets d’autrement prédéfinis, par conséquent, vous pouvez vous concentrer sur l’obtention de tout fonctionne.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-364">This package comes complete with a scene, with all objects in that prebuilt, so you can focus on getting it all working.</span></span> <span data-ttu-id="8e7b0-365">Le **ShelfKeeper** script est fourni, mais ne conserve que les variables publiques, à des fins de structure de programme d’installation de scène.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-365">The **ShelfKeeper** script is provided, though only holds the public variables, for the purpose of scene setup structure.</span></span> <span data-ttu-id="8e7b0-366">Vous devez effectuer toutes les autres sections.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-366">You will need to do all other sections.</span></span> 

<span data-ttu-id="8e7b0-367">Pour importer ce package :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-367">To import this package:</span></span>

1.  <span data-ttu-id="8e7b0-368">Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package, le Package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-368">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package, Custom Package**.</span></span>

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-39.png)

2.  <span data-ttu-id="8e7b0-370">Utilisez le sélecteur de fichiers pour sélectionner le **Azure-MR-307.unitypackage** du package et cliquez sur **Open**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-370">Use the file picker to select the **Azure-MR-307.unitypackage** package and click **Open**.</span></span>

3.  <span data-ttu-id="8e7b0-371">Une liste des composants de cette ressource s’affichera pour vous.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-371">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="8e7b0-372">Confirmez l’importation en cliquant sur **importer**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-372">Confirm the import by clicking **Import**.</span></span>

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-40.png)

4.  <span data-ttu-id="8e7b0-374">Une fois l’importation terminée, vous remarquerez que certains nouveaux dossiers apparues dans votre Unity **panneau projet**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-374">Once it has finished importing, you will notice that some new folders have appeared in your Unity **Project Panel**.</span></span> <span data-ttu-id="8e7b0-375">Ce sont les modèles 3D et les matériaux respectifs qui font partie de la scène prédéfinie, sur que vous allez travailler.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-375">Those are the 3D models and the respective materials that are part of the pre-made scene you will work on.</span></span> <span data-ttu-id="8e7b0-376">Vous allez écrire la majorité du code dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-376">You will write the majority of the code in this course.</span></span>

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-41.png)

5.  <span data-ttu-id="8e7b0-378">Dans le **panneau projet** dossier, cliquez sur le **scènes** dossier et double cliquez sur la scène à l’intérieur (appelé **MR_MachineLearningScene**).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-378">Within the **Project Panel** folder, click on the **Scenes** folder and double click on the scene inside (called **MR_MachineLearningScene**).</span></span> <span data-ttu-id="8e7b0-379">La scène s’ouvre (voir l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-379">The scene will open (see image below).</span></span> <span data-ttu-id="8e7b0-380">Si les losanges rouge sont manquants, cliquez simplement sur le **Gizmos** bouton, dans la partie supérieure droite de la **Panneau de jeu**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-380">If the red diamonds are missing, simply click the **Gizmos** button, at the top right of the **Game Panel**.</span></span>

    ![Importation du Package MLProducts Unity](images/AzureLabs-Lab7-44.png)

## <a name="chapter-7---checking-the-dlls-in-unity"></a><span data-ttu-id="8e7b0-382">Chapitre 7 - vérification des DLL dans Unity</span><span class="sxs-lookup"><span data-stu-id="8e7b0-382">Chapter 7 - Checking the DLLs in Unity</span></span>

<span data-ttu-id="8e7b0-383">Pour tirer parti de l’utilisation des bibliothèques JSON (utilisé pour sérialiser et désérialiser), une DLL Newtonsoft a été implémentée avec le package dans que vous est proposée.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-383">To leverage the use of JSON libraries (used for serializing and deserializing), a Newtonsoft DLL has been implemented with the package you brought in.</span></span> <span data-ttu-id="8e7b0-384">La bibliothèque doit avoir la configuration correcte, même si elle est valent (en particulier si vous rencontrez des problèmes avec le code ne fonctionne ne pas).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-384">The library should have the correct configuration, though it is worth checking (particularly if you are having issues with code not working).</span></span> 

<span data-ttu-id="8e7b0-385">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-385">To do so:</span></span>

-  <span data-ttu-id="8e7b0-386">Cliquez sur le fichier Newtonsoft dans le dossier de plug-ins et examinez le **panneau Inspecteur**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-386">Left-click on the Newtonsoft file inside the Plugins folder and look at the **Inspector panel**.</span></span> <span data-ttu-id="8e7b0-387">Assurez-vous que **Any plateforme** est coché.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-387">Make sure **Any Platform** is ticked.</span></span> <span data-ttu-id="8e7b0-388">Accédez à la **onglet UWP** et vérifiez également **ne pas traiter les** est coché.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-388">Go to the **UWP tab** and also ensure **Don't process** is ticked.</span></span>

    ![L’importation des DLL dans Unity](images/AzureLabs-Lab7-48.png)

## <a name="chapter-8---create-the-shelfkeeper-class"></a><span data-ttu-id="8e7b0-390">Chapitre 8 - créer la classe ShelfKeeper</span><span class="sxs-lookup"><span data-stu-id="8e7b0-390">Chapter 8 - Create the ShelfKeeper class</span></span>

<span data-ttu-id="8e7b0-391">Le **ShelfKeeper** classe héberge des méthodes qui contrôlent l’interface utilisateur et les produits générés dans la scène.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-391">The **ShelfKeeper** class hosts methods that control the UI and products spawned in the scene.</span></span>

<span data-ttu-id="8e7b0-392">Dans le cadre du package importé, vous vous ont été données cette classe, même si elle est incomplète.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-392">As part of the imported package, you will have been given this class, though it is incomplete.</span></span> <span data-ttu-id="8e7b0-393">Il est maintenant temps de terminer cette classe :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-393">It is now time to complete that class:</span></span>

1.  <span data-ttu-id="8e7b0-394">Double-cliquez sur le **ShelfKeeper** de script, dans le **Scripts** dossier, pour l’ouvrir avec **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-394">Double click on the **ShelfKeeper** script, within the **Scripts** folder, to open it with **Visual Studio 2017**.</span></span>

2.  <span data-ttu-id="8e7b0-395">Remplacez tout le code existant dans le script avec le code suivant, qui définit la date et l’heure et dispose d’une méthode pour afficher un produit.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-395">Replace all the code existing in the script with the following code, which sets the time and date and has a method to show a product.</span></span>

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

3.  <span data-ttu-id="8e7b0-396">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-396">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

4.  <span data-ttu-id="8e7b0-397">Revenez dans l’éditeur Unity, vérifiez que le **ShelfKeeper** classe ressemble à la ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-397">Back in the Unity Editor, check that the **ShelfKeeper** class looks like the below:</span></span>

    ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-51.png)

    > [!IMPORTANT]
    > <span data-ttu-id="8e7b0-399">Si votre script n’a pas les cibles de référence (par exemple, *Date (texte de maillage)*), faites simplement glisser les objets correspondants de la **hiérarchie panneau**, dans les champs de la cible.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-399">If your script does not have the reference targets (i.e. *Date (Text Mesh)*), simply drag the corresponding objects from the **Hierarchy Panel**, into the target fields.</span></span> <span data-ttu-id="8e7b0-400">Voir ci-dessous pour savoir plus, si nécessaire :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-400">See below for explanation, if needed:</span></span>
    > 
    > 1.  <span data-ttu-id="8e7b0-401">Ouvrez le **Spawn Point** de tableau dans le **ShelfKeeper** script composant par clic gauche il.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-401">Open the **Spawn Point** array within the **ShelfKeeper** component script by left-clicking it.</span></span> <span data-ttu-id="8e7b0-402">Une sous-section apparaît appelée **taille**, ce qui indique la taille du tableau.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-402">A sub-section will appear called **Size**, which indicates the size of the array.</span></span> <span data-ttu-id="8e7b0-403">Type **3** dans la zone de texte suivant pour **taille** et appuyez sur **entrée**, et trois emplacements seront créés sous.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-403">Type **3** into the textbox next to **Size** and press **Enter**, and three slots will be created beneath.</span></span>
    > 2. <span data-ttu-id="8e7b0-404">Dans le **hiérarchie** développez la **affichage temps** objet (en cliquant dessus à la flèche en regard de celle-ci).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-404">Within the **Hierarchy** expand the **Time Display** object (by left-clicking the arrow beside it).</span></span> <span data-ttu-id="8e7b0-405">Ensuite cliquez sur le ***Main Camera*** depuis le **hiérarchie**, de sorte que le **inspecteur** montre ses informations.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-405">Next click the ***Main Camera*** from within the **Hierarchy**, so that the **Inspector** shows its information.</span></span>
    > 3. <span data-ttu-id="8e7b0-406">Sélectionnez le **caméra principale** dans le **hiérarchie panneau**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-406">Select the **Main Camera** in the **Hierarchy Panel**.</span></span> <span data-ttu-id="8e7b0-407">Faites glisser le **Date** et **temps** objets à partir de la **Panneau de la hiérarchie** à la **texte de la Date** et **texte moment** emplacements au sein de la **inspecteur** de la **Main Camera** dans le **ShelfKeeper** composant.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-407">Drag the **Date** and **Time** objects from the **Hierarchy Panel** to the **Date Text** and **Time Text** slots within the **Inspector** of the **Main Camera** in the **ShelfKeeper** component.</span></span>
    > 4. <span data-ttu-id="8e7b0-408">Faites glisser le **Spawn Points** à partir de la **Panneau de la hiérarchie** (sous le *étagère* objet) à la **3** **élément**référence cibles sous le **Spawn Point** de tableau, comme indiqué dans l’image.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-408">Drag the **Spawn Points** from the **Hierarchy Panel** (beneath the *Shelf* object) to the **3** **Element** reference targets beneath the **Spawn Point** array, as shown in the image.</span></span>
    > 
    >     ![Créer la classe ShelfKeeper](images/AzureLabs-Lab7-52.png)

## <a name="chapter-9---create-the-productprediction-class"></a><span data-ttu-id="8e7b0-410">Chapitre 9 - créer la classe ProductPrediction</span><span class="sxs-lookup"><span data-stu-id="8e7b0-410">Chapter 9 - Create the ProductPrediction class</span></span>

<span data-ttu-id="8e7b0-411">La classe suivante, vous allez créer est la **ProductPrediction** classe.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-411">The next class you are going to create is the **ProductPrediction** class.</span></span>

<span data-ttu-id="8e7b0-412">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-412">This class is responsible for:</span></span>

-   <span data-ttu-id="8e7b0-413">Interrogation de la **Service Machine Learning** instance, qui fournit la date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-413">Querying the **Machine Learning Service** instance, providing the current date and time.</span></span>

-   <span data-ttu-id="8e7b0-414">La désérialisation de la réponse JSON en données exploitables.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-414">Deserializing the JSON response into usable data.</span></span>

-   <span data-ttu-id="8e7b0-415">Interprétation des données, récupérer les produits recommandés 3.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-415">Interpreting the data, retrieving the 3 recommended products.</span></span>

-   <span data-ttu-id="8e7b0-416">Appel de la **ShelfKeeper** méthodes pour afficher les données dans la scène de la classe.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-416">Calling the **ShelfKeeper** class methods to display the data in the Scene.</span></span>

<span data-ttu-id="8e7b0-417">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-417">To create this class:</span></span>

1.  <span data-ttu-id="8e7b0-418">Accédez à la **Scripts** dossier, dans le **panneau projet**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-418">Go to the **Scripts** folder, in the **Project Panel**.</span></span>

2.  <span data-ttu-id="8e7b0-419">Avec le bouton droit dans le dossier, **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-419">Right-click inside the folder, **Create** > **C\# Script**.</span></span> <span data-ttu-id="8e7b0-420">Appeler le script **ProductPrediction**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-420">Call the script **ProductPrediction**.</span></span>

3.  <span data-ttu-id="8e7b0-421">Double-cliquez sur le nouveau **ProductPrediction** script pour l’ouvrir avec **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-421">Double click on the new **ProductPrediction** script to open it with **Visual Studio 2017**.</span></span>

4.  <span data-ttu-id="8e7b0-422">Si le **Modification de fichier détectée** boîte de dialogue s’affiche, cliquez sur \***recharger la Solution**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-422">If the **File Modification Detected** dialog pops up, click \***Reload Solution**.</span></span>

5.  <span data-ttu-id="8e7b0-423">Ajoutez les espaces de noms suivantes au début de la classe ProductPrediction :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-423">Add the following namespaces to the top of the ProductPrediction class:</span></span>

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

6.  <span data-ttu-id="8e7b0-424">À l’intérieur de la **ProductPrediction** classe insérer les deux objets suivants qui sont composées d’un nombre de classes imbriquées.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-424">Inside the **ProductPrediction** class insert the following two objects which are composed of a number of nested classes.</span></span> <span data-ttu-id="8e7b0-425">Ces classes sont utilisées pour sérialiser et désérialiser l’objet JSON pour le Service Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-425">These classes are used to serialize and deserialize the JSON for the Machine Learning Service.</span></span>

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

7.  <span data-ttu-id="8e7b0-426">Puis ajoutez les variables suivantes au-dessus du code précédent (afin que le JSON liés code figure au bas du script, tous les autres code ci-dessous et en dehors de la façon) :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-426">Then add the following variables above the previous code (so that the JSON related code is at the bottom of the script, below all other code, and out of the way):</span></span>

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
    > <span data-ttu-id="8e7b0-427">Veillez à insérer le **clé primaire** et **point de terminaison de requête-réponse**, à partir du portail de formation Machine, dans les variables ici.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-427">Make sure to insert the **primary key** and **request-response endpoint**, from the Machine Learning Portal, into the variables here.</span></span> <span data-ttu-id="8e7b0-428">Les images ci-après montrent où vous aurait fallu la clé et le point de terminaison.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-428">The below images show where you would have taken the key and endpoint from.</span></span> 
    >  
    > ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-53-1.png)
    >
    > ![Machine Learning Studio : L’expérience](images/AzureLabs-Lab7-53-2.png)

8.  <span data-ttu-id="8e7b0-431">Insérez ce code dans le **Start()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-431">Insert this code within the **Start()** method.</span></span> <span data-ttu-id="8e7b0-432">Le **Start()** méthode est appelée lors de l’initialisation de la classe :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-432">The **Start()** method is called when the class initializes:</span></span>

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

9.  <span data-ttu-id="8e7b0-433">Voici la méthode qui Récupère la date et l’heure à partir de Windows et le convertit en un format que notre expérience d’apprentissage Machine peut utiliser pour comparer avec les données stockées dans la table.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-433">The following is the method that collects the date and time from Windows and converts it into a format that our Machine Learning Experiment can use to compare with the data stored in the table.</span></span>

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

10. <span data-ttu-id="8e7b0-434">Vous pouvez **supprimer** le **Update()** étant donné que cette classe ne l’utilise pas de méthode.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-434">You can **delete** the **Update()** method since this class will not use it.</span></span>

11. <span data-ttu-id="8e7b0-435">Ajoutez la méthode suivante qui sera de communiquer la date et heure actuelles au point de terminaison Machine Learning et de recevoir une réponse au format JSON.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-435">Add the following method which will communicate the current date and time to the Machine Learning endpoint and receive a response in JSON format.</span></span>

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

12. <span data-ttu-id="8e7b0-436">Ajoutez la méthode suivante, qui est responsable de la désérialisation de la réponse JSON et communique le résultat de la désérialisation pour le **ShelfKeeper** classe.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-436">Add the following method, which is responsible for deserializing the JSON response, and communicating the result of the deserialization to the **ShelfKeeper** class.</span></span> <span data-ttu-id="8e7b0-437">Ce résultat sera les noms des trois éléments prévues de vendre le plus à la date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-437">This result will be the names of the three items predicted to sell the most at current date and time.</span></span> <span data-ttu-id="8e7b0-438">Insérez le code ci-dessous dans le **ProductPrediction** (classe), sous la méthode précédente.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-438">Insert the code below into the **ProductPrediction** class, below the previous method.</span></span>

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

13. <span data-ttu-id="8e7b0-439">Enregistrer **Visual Studio** et revenez **Unity**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-439">Save **Visual Studio** and head back to **Unity**.</span></span>

14. <span data-ttu-id="8e7b0-440">Faites glisser le **ProductPrediction** classe le script à partir de la **Script** dossier, sur le **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-440">Drag the **ProductPrediction** class script from the **Script** folder, onto the **Main Camera** object.</span></span>

15. <span data-ttu-id="8e7b0-441">Enregistrer votre projet et scène **fichier** > ***enregistrer la scène* / *fichier***   >  **Enregistrer le projet**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-441">Save your scene and project **File** > ***Save Scene* / *File*** > **Save Project**.</span></span>

## <a name="chapter-10---build-the-uwp-solution"></a><span data-ttu-id="8e7b0-442">Chapitre 10 - générer la Solution UWP</span><span class="sxs-lookup"><span data-stu-id="8e7b0-442">Chapter 10 - Build the UWP Solution</span></span>

<span data-ttu-id="8e7b0-443">Il est maintenant temps de générer votre projet comme une solution UWP, afin qu’il peut s’exécuter comme une application autonome.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-443">It is now time to build your project as a UWP solution, so that it can run as a standalone application.</span></span>

<span data-ttu-id="8e7b0-444">Pour générer :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-444">To Build:</span></span>

1.  <span data-ttu-id="8e7b0-445">Enregistrer la scène actuelle en cliquant sur **fichier** **enregistrer les scènes**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-445">Save the current scene by clicking on **File** **Save Scenes**.</span></span>

2.  <span data-ttu-id="8e7b0-446">Accédez à **fichier** **les paramètres de génération**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-446">Go to **File** **Build Settings**</span></span>

3.  <span data-ttu-id="8e7b0-447">Cochez la case appelée **Unity C\# projets** (Ceci est important, car il vous permettra de modifier les classes après de la build est terminée).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-447">Check the box called **Unity C\# Projects** (this is important because it will allow you to edit the classes after build is completed).</span></span>

4.  <span data-ttu-id="8e7b0-448">Cliquez sur **ajouter des scènes Open**,</span><span class="sxs-lookup"><span data-stu-id="8e7b0-448">Click on **Add Open Scenes**,</span></span>

5.  <span data-ttu-id="8e7b0-449">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-449">Click **Build**.</span></span>

    ![Générez la Solution UWP](images/AzureLabs-Lab7-54.png)

6.  <span data-ttu-id="8e7b0-451">Vous êtes invité à sélectionner le dossier dans lequel vous souhaitez générer la Solution.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-451">You will be prompted to select the folder where you want to build the Solution.</span></span>

7.  <span data-ttu-id="8e7b0-452">Créer un **génère** dossier et dans ce dossier, créez un autre dossier avec un nom approprié de votre choix.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-452">Create a **BUILDS** folder and within that folder create another folder with an appropriate name of your choice.</span></span>

8.  <span data-ttu-id="8e7b0-453">Cliquez sur votre nouveau dossier, puis **sélectionner le dossier**à commencer la build à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-453">Click your new folder and then click **Select Folder**, to begin the build at that location.</span></span>

    ![Générez la Solution UWP](images/AzureLabs-Lab7-55.png)

    ![Générez la Solution UWP](images/AzureLabs-Lab7-56.png)

9.  <span data-ttu-id="8e7b0-456">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="8e7b0-456">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

## <a name="chapter-11---deploy-your-application"></a><span data-ttu-id="8e7b0-457">Chapitre 11 - déployer votre Application</span><span class="sxs-lookup"><span data-stu-id="8e7b0-457">Chapter 11 - Deploy your Application</span></span>

<span data-ttu-id="8e7b0-458">Pour déployer votre application :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-458">To deploy your application:</span></span>

1.  <span data-ttu-id="8e7b0-459">Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-459">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

2.  <span data-ttu-id="8e7b0-460">Visual Studio ouvert, vous devez restaurer les Packages NuGet, ce qui peut être effectué via un clic droit sur votre solution MachineLearningLab_Build, à partir de l’Explorateur de solutions (situé à droite de Visual Studio), puis cliquez sur Restaurer les Packages NuGet :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-460">With Visual Studio open, you need to Restore NuGet Packages, which can be done through right-clicking your MachineLearningLab_Build solution, from the Solution Explorer (found to the right of Visual Studio), and then clicking Restore NuGet Packages:</span></span>

    ![Ajout de Packages NuGet](images/AzureLabs-Lab7-57.png)

3.  <span data-ttu-id="8e7b0-462">Dans, sélectionnez la Configuration de Solution **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-462">In the Solution Configuration select **Debug**.</span></span>

4.  <span data-ttu-id="8e7b0-463">Dans la plateforme de Solution, sélectionnez **x86**, **ordinateur Local**.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-463">In the Solution Platform, select **x86**, **Local Machine**.</span></span> 

    > <span data-ttu-id="8e7b0-464">Pour le Microsoft HoloLens, il peut s’avérer plus facile d’affecter à ce *Machine distante*, de sorte que vous ne sont pas attachés à votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-464">For the Microsoft HoloLens, you may find it easier to set this to *Remote Machine*, so that you are not tethered to your computer.</span></span> <span data-ttu-id="8e7b0-465">Cependant, vous devez également effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="8e7b0-465">Though, you will need to also do the following:</span></span>
    > - <span data-ttu-id="8e7b0-466">Connaître le **adresse IP** de votre HoloLens, ce qui se trouve dans le *Paramètres > réseau & Internet > Wi-Fi > Options avancées*; IPv4 est l’adresse que vous devez utiliser.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-466">Know the **IP Address** of your HoloLens, which can be found within the *Settings > Network & Internet > Wi-Fi > Advanced Options*; the IPv4 is the address you should use.</span></span> 
    > - <span data-ttu-id="8e7b0-467">Vérifiez **Mode développeur** est **sur**; trouvé dans *Paramètres > mise à jour & sécurité > pour les développeurs*.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-467">Ensure **Developer Mode** is **On**; found in *Settings > Update & Security > For developers*.</span></span>

    ![Ajout de Packages NuGet](images/AzureLabs-Lab7-58.png)

5.  <span data-ttu-id="8e7b0-469">Accédez à **menu Générer** , puis cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre PC.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-469">Go to **Build menu** and click on **Deploy Solution** to sideload the application to your PC.</span></span>

6.  <span data-ttu-id="8e7b0-470">Votre application doit maintenant apparaître dans la liste des applications installées, prêtes à être lancée.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-470">Your App should now appear in the list of installed apps, ready to be launched.</span></span>

<span data-ttu-id="8e7b0-471">Lorsque vous exécutez l’application de réalité mixte, vous verrez le banc qui a été configuré dans votre scène Unity, et à partir de l’initialisation, seront extraites les données que vous configurez dans Azure.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-471">When you run the Mixed Reality application, you will see the bench that was set up in your Unity scene, and from initialization, the data you set up within Azure will be fetched.</span></span> <span data-ttu-id="8e7b0-472">Les données seront désérialisées au sein de votre application, et fournirons visuellement, en tant que trois modèles sur le banc les trois premiers résultats pour votre date et heure actuelles.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-472">The data will be deserialized within your application, and the three top results for your current date and time will be provided visually, as three models on the bench.</span></span>


## <a name="your-finished-machine-learning-application"></a><span data-ttu-id="8e7b0-473">Votre application de Machine Learning terminée</span><span class="sxs-lookup"><span data-stu-id="8e7b0-473">Your finished Machine Learning application</span></span>
 
<span data-ttu-id="8e7b0-474">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’Azure Machine Learning pour effectuer des prédictions de données et l’afficher dans votre scène.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-474">Congratulations, you built a mixed reality app that leverages the Azure Machine Learning to make data predictions and display it on your scene.</span></span>

![Ajout de Packages NuGet](images/AzureLabs-Lab7-0.png)

## <a name="exercise"></a><span data-ttu-id="8e7b0-476">Exercice</span><span class="sxs-lookup"><span data-stu-id="8e7b0-476">Exercise</span></span>

<span data-ttu-id="8e7b0-477">**Exercice 1**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-477">**Exercise 1**</span></span>

<span data-ttu-id="8e7b0-478">Faire des essais avec l’ordre de tri de votre application et afficher les prédictions de trois bas en rayon, comme ces données potentiellement serait utiles également.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-478">Experiment with the sort order of your application and have the three bottom predictions appear on the shelf, as this data would potentially be useful also.</span></span>

<span data-ttu-id="8e7b0-479">**Exercice 2**</span><span class="sxs-lookup"><span data-stu-id="8e7b0-479">**Exercise 2**</span></span>

<span data-ttu-id="8e7b0-480">À l’aide de **Tables Azure** remplir une nouvelle table avec les informations météorologiques et créer une expérience à l’aide de données.</span><span class="sxs-lookup"><span data-stu-id="8e7b0-480">Using **Azure Tables** populate a new table with weather information and create a new experiment using the data.</span></span>
