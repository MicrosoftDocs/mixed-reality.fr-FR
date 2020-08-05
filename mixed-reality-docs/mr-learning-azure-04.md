---
title: Tutoriels sur le cloud Azure - 4. Intégration d’Azure Spatial Anchors
description: Suivez ce cours pour découvrir comment implémenter Azure Spatial Anchors dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 07/01/2020
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, ancres spatiales Azure
ms.localizationpriority: high
ms.openlocfilehash: 468ba0d8e9fca85dc266b662f402f5c956dc94bb
ms.sourcegitcommit: 2f5f95a9ca1b02d94eb9163f0f4ff6b1e4126de2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87376441"
---
# <a name="4-integrating-azure-spatial-anchors"></a><span data-ttu-id="07dd5-105">4. Intégration d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="07dd5-105">4. Integrating Azure Spatial Anchors</span></span>

<span data-ttu-id="07dd5-106">Dans ce tutoriel, vous allez découvrir comment utiliser **Azure Spatial Anchors**.</span><span class="sxs-lookup"><span data-stu-id="07dd5-106">In this tutorial, you will learn how to use **Azure Spatial Anchors**.</span></span> <span data-ttu-id="07dd5-107">Vous allez stocker l’emplacement d’un **objet suivi** en tant qu’ancre spatiale Azure.</span><span class="sxs-lookup"><span data-stu-id="07dd5-107">You will store the location of a **Tracked Object** as an Azure Spatial Anchor.</span></span> <span data-ttu-id="07dd5-108">Ensuite, vous interrogerez et présenterez à l’utilisateur une flèche de guidage pointant vers l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="07dd5-108">Then you will query and present the user with a guiding arrow pointing to the location.</span></span>

## <a name="objectives"></a><span data-ttu-id="07dd5-109">Objectifs</span><span class="sxs-lookup"><span data-stu-id="07dd5-109">Objectives</span></span>

* <span data-ttu-id="07dd5-110">Apprendre les bases d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="07dd5-110">Learn the basics of Azure Spatial Anchors.</span></span>
* <span data-ttu-id="07dd5-111">Apprendre à configurer la scène pour utiliser Azure Spatial Anchors dans ce projet</span><span class="sxs-lookup"><span data-stu-id="07dd5-111">Learn how to set up the scene to use Azure Spatial Anchors in this project.</span></span>
* <span data-ttu-id="07dd5-112">Apprendre à intégrer le stockage et la recherche des emplacements</span><span class="sxs-lookup"><span data-stu-id="07dd5-112">Learn how to integrate storing and querying locations.</span></span>

## <a name="understanding-azure-spatial-anchors"></a><span data-ttu-id="07dd5-113">Présentation d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="07dd5-113">Understanding Azure Spatial Anchors</span></span>

 <span data-ttu-id="07dd5-114">**Azure Spatial Anchors** fait partie de la famille Azure Cloud Services. Sa fonction est d’enregistrer les emplacements d’ancrage.</span><span class="sxs-lookup"><span data-stu-id="07dd5-114">**Azure Spatial Anchors** is part of the Azure Cloud Services family and is used to save anchor locations.</span></span> <span data-ttu-id="07dd5-115">Les emplacements d’ancrage enregistrés peuvent être récupérés à partir du cloud d’après l’*ID d’ancre*.</span><span class="sxs-lookup"><span data-stu-id="07dd5-115">The saved anchor locations can be retrieved based on the *anchor ID* from the cloud.</span></span> <span data-ttu-id="07dd5-116">Ces emplacements d’ancrage peuvent être partagés et sollicités par des appareils multiplateformes tels que des appareils HoloLens, iOS et Android.</span><span class="sxs-lookup"><span data-stu-id="07dd5-116">This anchor location can be shared and accessed by multi-platform devices like HoloLens, iOS, and Android devices.</span></span>

<span data-ttu-id="07dd5-117">Apprenez-en davantage sur [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview).</span><span class="sxs-lookup"><span data-stu-id="07dd5-117">Learn more about [Azure Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/overview).</span></span>

## <a name="preparing-azure-spatial-anchors"></a><span data-ttu-id="07dd5-118">Préparation d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="07dd5-118">Preparing Azure Spatial Anchors</span></span>

<span data-ttu-id="07dd5-119">Avant de commencer, vous devez créer une ressource Spatial Anchors dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="07dd5-119">Before you can start, you have to create a spatial anchor resource in your Azure portal.</span></span>
<span data-ttu-id="07dd5-120">Découvrez comment créer une [ressource Spatial Anchors](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource).</span><span class="sxs-lookup"><span data-stu-id="07dd5-120">Learn how to make a [spatial anchor resource](https://docs.microsoft.com/azure/spatial-anchors/quickstarts/get-started-hololens#create-a-spatial-anchors-resource).</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="07dd5-121">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="07dd5-121">Preparing the scene</span></span>

<span data-ttu-id="07dd5-122">Dans cette section, vous allez découvrir comment configurer la scène et apporter les modifications nécessaires.</span><span class="sxs-lookup"><span data-stu-id="07dd5-122">In this section, you will learn how to configure the scene and make the necessary changes.</span></span>

<span data-ttu-id="07dd5-123">Dans la fenêtre Project, accédez à **Assets > MRTK.Tutorials.AzureCloudServices > Prefabs > Manager**.</span><span class="sxs-lookup"><span data-stu-id="07dd5-123">In the Project window, navigate to the **Assets > MRTK.Tutorials.AzureCloudServices > Prefabs > Manager**</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step1-1.png)

<span data-ttu-id="07dd5-125">Dans le dossier **Manager**, glissez-déposez le préfabriqué **Anchor Manager** vers la hiérarchie de la scène.</span><span class="sxs-lookup"><span data-stu-id="07dd5-125">From the **Manager** folder, drag and drop the prefab **Anchor Manager** into the scene Hierarchy.</span></span>

<span data-ttu-id="07dd5-126">Sélectionnez **Anchor Manager** GameObject dans la hiérarchie et, dans la section Inspector, vous trouverez **Spatial Anchor Manager** (Script).</span><span class="sxs-lookup"><span data-stu-id="07dd5-126">Select **Anchor Manager** GameObject in the Hierarchy, and in the Inspector section, you will find **Spatial Anchor Manager** (Script).</span></span> <span data-ttu-id="07dd5-127">Recherchez l’ID de compte et le champ de clé, puis ajoutez les informations d’identification que vous avez créées dans la section Prérequis à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="07dd5-127">Find account ID and key field and add the credentials which you had created in the prerequisite in the earlier stage.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step2-1.png)

<span data-ttu-id="07dd5-129">À présent, recherchez l’objet **Scene Controller** dans la hiérarchie de votre scène et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="07dd5-129">Now find the **Scene Controller** object in your scene Hierarchy and select it.</span></span> <span data-ttu-id="07dd5-130">Vous verrez l’inspecteur **Scene Controller**.</span><span class="sxs-lookup"><span data-stu-id="07dd5-130">You will see the **Scene Controller** Inspector.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial4-section1-step3-1.png)

<span data-ttu-id="07dd5-132">Vous remarquerez que le champ **Anchor Manager** du composant **Scene Controller** est vide. Glissez-déposez l’**Anchor Manager** de la hiérarchie de la scène vers ce champ et enregistrez la scène.</span><span class="sxs-lookup"><span data-stu-id="07dd5-132">You will observe that the **Anchor Manager** field in the **Scene Controller** component is empty, drag and drop the **Anchor Manager** from the Hierarchy in the scene into that field and save the scene.</span></span>

## <a name="build-and-deploy-the-app-to-your-hololens-2"></a><span data-ttu-id="07dd5-133">Générer et déployer l’application sur votre HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="07dd5-133">Build and Deploy the app to your HoloLens 2</span></span>

<span data-ttu-id="07dd5-134">Azure Spatial Anchors ne peut pas s’exécuter dans Unity : pour tester la fonctionnalité Azure Spatial Anchors, vous devez déployer le projet sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="07dd5-134">Azure Spatial Anchors can not run in Unity, so to test the Azure Spatial Anchors functionality, you need to deploy the project to your device.</span></span>

> [!TIP]
> <span data-ttu-id="07dd5-135">Pour vous rappeler comment générer et déployer votre projet Unity sur HoloLens 2, reportez-vous aux instructions fournies dans [Génération de votre application sur votre HoloLens 2](mr-learning-base-02.md#building-your-application-to-your-hololens-2).</span><span class="sxs-lookup"><span data-stu-id="07dd5-135">For a reminder on how to build and deploy your Unity project to HoloLens 2, you can refer to the [Building your application to your HoloLens 2](mr-learning-base-02.md#building-your-application-to-your-hololens-2) instructions.</span></span>

## <a name="run-the-app-on-your-hololens-2-and-follow-the-in-app-instructions"></a><span data-ttu-id="07dd5-136">Exécuter l’application sur votre HoloLens 2 et suivre les instructions dans l’application</span><span class="sxs-lookup"><span data-stu-id="07dd5-136">Run the app on your HoloLens 2 and follow the in-app instructions</span></span>

### <a name="create-an-anchor-to-store-a-location"></a><span data-ttu-id="07dd5-137">Créer une ancre où stocker un emplacement</span><span class="sxs-lookup"><span data-stu-id="07dd5-137">Create an anchor to store a location</span></span>

<span data-ttu-id="07dd5-138">Dans cette section, vous allez découvrir comment enregistrer l’emplacement d’un objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-138">In this section you will see how to save the object location.</span></span>

<span data-ttu-id="07dd5-139">Exécutez l’application et cliquez sur **Set Object** (Définir un objet) dans le menu principal de l’expérience.</span><span class="sxs-lookup"><span data-stu-id="07dd5-139">Run the application and click on **Set Object** in the main menu of the experience.</span></span>

<span data-ttu-id="07dd5-140">Indiquez le **nom** de l’objet que vous souhaitez enregistrer, puis cliquez sur **Set Object** pour continuer.</span><span class="sxs-lookup"><span data-stu-id="07dd5-140">Give the **name** of the object you want to save and click on **Set Object** to continue.</span></span> <span data-ttu-id="07dd5-141">Pour ajouter des informations supplémentaires sur l’objet, sélectionnez l’**image** et décrivez l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-141">To add more information about the object, select the **image**, and describe the object.</span></span>

<span data-ttu-id="07dd5-142">Pour enregistrer l’emplacement, cliquez sur **Save Location**.</span><span class="sxs-lookup"><span data-stu-id="07dd5-142">To save the location, click on **Save Location**</span></span>

<span data-ttu-id="07dd5-143">Vous verrez un **pointeur d’ancrage** que vous pouvez déplacer et positionner à l’emplacement que vous souhaitez enregistrer.</span><span class="sxs-lookup"><span data-stu-id="07dd5-143">You will see an **anchor pointer** that you can move and place on the location you want to save.</span></span> <span data-ttu-id="07dd5-144">Après cela, une fenêtre contextuelle de confirmation s’affiche.</span><span class="sxs-lookup"><span data-stu-id="07dd5-144">After that, you will get a confirmation popup.</span></span> <span data-ttu-id="07dd5-145">Si vous souhaitez confirmer et enregistrer l’emplacement, cliquez sur **Yes** ; dans le cas contraire, vous pouvez changer l’emplacement en cliquant sur **No** et en sélectionnant à nouveau l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="07dd5-145">If you want to confirm and save the location, click on **Yes**; otherwise, you can change the location by clicking on **No** and selecting the location again.</span></span>

<span data-ttu-id="07dd5-146">Une fois que vous avez confirmé l’emplacement en cliquant sur **Yes**, l’emplacement et l’ID d’ancre sont enregistrés dans le stockage cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="07dd5-146">Once you confirm the location by clicking on **Yes**, the location and the Anchor ID will be saved in the Azure cloud storage.</span></span> <span data-ttu-id="07dd5-147">Après cela, vous verrez l’**étiquette d’objet** dans l’ancre, avec le nom de l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-147">Once it is saved, you will see the **Object tag**  in the anchor with the object's name.</span></span>

<span data-ttu-id="07dd5-148">L’emplacement de l’objet est maintenant enregistré.</span><span class="sxs-lookup"><span data-stu-id="07dd5-148">Now the object location is saved successfully.</span></span>

### <a name="query-for-finding-an-anchor-location"></a><span data-ttu-id="07dd5-149">Recherche d’un emplacement d’ancrage</span><span class="sxs-lookup"><span data-stu-id="07dd5-149">Query for finding an anchor location</span></span>

<span data-ttu-id="07dd5-150">Une fois que vous avez enregistré correctement l’emplacement d’ancrage, vous pouvez le rechercher en sélectionnant **Search Object** dans le menu principal.</span><span class="sxs-lookup"><span data-stu-id="07dd5-150">Once after you successfully saved the anchor location, now you can find the anchor location by selecting **Search Object** in the main menu.</span></span>

<span data-ttu-id="07dd5-151">Quand vous cliquez sur **Search Object**, une nouvelle fenêtre s’affiche, dans laquelle vous devez indiquer le nom de l’objet à rechercher.</span><span class="sxs-lookup"><span data-stu-id="07dd5-151">After clicking on **Search Object**, a new window will pop up in which you should give the name of the object you want to search.</span></span>

<span data-ttu-id="07dd5-152">Entrez le nom de l’objet et cliquez sur **Search Object**.</span><span class="sxs-lookup"><span data-stu-id="07dd5-152">Enter the name of the object and click on **Search Object**.</span></span> <span data-ttu-id="07dd5-153">Si l’objet a été enregistré précédemment et se trouve dans la base de données, vous obtiendrez la fiche de l’objet avec tous les détails de l’objet que vous avez enregistré.</span><span class="sxs-lookup"><span data-stu-id="07dd5-153">If the object is saved previously and is found in the database, you will get the object card with all the details of the object you would have saved earlier.</span></span>

<span data-ttu-id="07dd5-154">Vous pouvez maintenant cliquer sur **Show Location** (Afficher l’emplacement) pour rechercher l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-154">Now you can click on **Show Location** to find the object.</span></span> <span data-ttu-id="07dd5-155">Quand vous cliquez sur **Show Location**, le système interroge le stockage cloud afin de connaître l’adresse de l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-155">Once you click on **Show Location**, the system will query the object address from the cloud storage.</span></span>

<span data-ttu-id="07dd5-156">Une fois l’emplacement récupéré, une **flèche** vous dirige vers l’emplacement de l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-156">After successfully retrieving the location, an **arrow** will direct you towards the location of the object.</span></span> <span data-ttu-id="07dd5-157">Suivez la flèche jusqu’à ce que vous trouviez l’emplacement de l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-157">Follow the arrow mark until you find the location of the object.</span></span>

<span data-ttu-id="07dd5-158">Une fois que vous avez trouvé l’objet, son nom s’affiche en haut et la flèche disparaît. Vous pouvez maintenant cliquer sur l’**étiquette d’objet** pour voir les détails de l’objet.</span><span class="sxs-lookup"><span data-stu-id="07dd5-158">Once you find the object, the object name will appear at the top, and the arrow mark will disappear, and now you can click on the **object tag** to see the details of the object.</span></span>

## <a name="congratulations"></a><span data-ttu-id="07dd5-159">Félicitations</span><span class="sxs-lookup"><span data-stu-id="07dd5-159">Congratulations</span></span>

<span data-ttu-id="07dd5-160">Dans ce tutoriel, vous avez vu comment Azure Spatial Anchors pouvait enregistrer et récupérer l’emplacement d’un objet sur HoloLense 2.</span><span class="sxs-lookup"><span data-stu-id="07dd5-160">In this tutorial, you learned how Azure Spatial Anchors could save and retrieve the object location on Hololense 2.</span></span>

<span data-ttu-id="07dd5-161">Dans le dernier tutoriel, vous allez découvrir comment utiliser **Azure Bot Service** pour ajouter le langage naturel comme nouvelle méthode d’interaction pour notre application.</span><span class="sxs-lookup"><span data-stu-id="07dd5-161">In the final tutorial, you will learn how to use the **Azure Bot Service** to add natural language as a new interaction method for our application.</span></span>

[<span data-ttu-id="07dd5-162">Tutoriel suivant : 5. Intégration d’Azure Bot Service avec LUIS</span><span class="sxs-lookup"><span data-stu-id="07dd5-162">Next tutorial: 5. Integrating Azure Bot Service with LUIS</span></span>](mr-learning-azure-05.md)