---
title: Tutoriels sur le cloud Azure - 3. Intégration d’Azure Custom Vision
description: Suivez ce cours pour découvrir comment implémenter Azure Custom Vision dans une application HoloLens 2.
author: jessemcculloch
ms.author: jemccull
ms.date: 02/26/2019
ms.topic: article
keywords: réalité mixte, unity, tutoriel, hololens, hololens 2, azure custom vision, azure cognitive services
ms.localizationpriority: high
ms.openlocfilehash: c3ba5a715b0e77d7869d598a472341cd390c2d23
ms.sourcegitcommit: 96ae8258539b2f3edc104dd0dce8bc66f3647cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86304532"
---
# <a name="3-integrating-azure-custom-vision"></a><span data-ttu-id="254db-105">3. Intégration d’Azure Custom Vision</span><span class="sxs-lookup"><span data-stu-id="254db-105">3. Integrating Azure Custom Vision</span></span>

<span data-ttu-id="254db-106">Dans ce tutoriel, vous allez apprendre à utiliser **Azure Custom Vision**. Vous allez charger un ensemble de photos pour l’associer à un *objet suivi*, les charger sur le service **Custom Vision** et démarrer le processus d’entraînement.</span><span class="sxs-lookup"><span data-stu-id="254db-106">In this tutorial, you will learn how to use **Azure Custom Vision**.You will upload a set of photos to associate it with a *Tracked Object*, upload them to the **Custom Vision** service and start the training process.</span></span> <span data-ttu-id="254db-107">Ensuite, vous utiliserez le service pour détecter l’*objet suivi* en capturant des photos à partir du flux de la webcam.</span><span class="sxs-lookup"><span data-stu-id="254db-107">Then you will use the service to detect the *Tracked Object* by capturing photos from the webcam feed.</span></span>

## <a name="objectives"></a><span data-ttu-id="254db-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="254db-108">Objectives</span></span>

* <span data-ttu-id="254db-109">Apprendre les bases d’Azure Custom Vision</span><span class="sxs-lookup"><span data-stu-id="254db-109">Learn the basics about Azure Custom Vision</span></span>
* <span data-ttu-id="254db-110">Apprendre à configurer la scène pour utiliser Custom Vision dans ce projet</span><span class="sxs-lookup"><span data-stu-id="254db-110">Learn how to setup the scene to use Custom Vision in this project</span></span>
* <span data-ttu-id="254db-111">Apprendre à intégrer les images de chargement, d’entraînement et de détection</span><span class="sxs-lookup"><span data-stu-id="254db-111">Learn how to integrate upload, train and detect images</span></span>

## <a name="understanding-azure-custom-vision"></a><span data-ttu-id="254db-112">Présentation d’Azure Custom Vision</span><span class="sxs-lookup"><span data-stu-id="254db-112">Understanding Azure Custom Vision</span></span>

<span data-ttu-id="254db-113">**Azure Custom Vision** fait partie de la famille **Cognitive Services** et est utilisé pour l’entraînement des classifieurs d’images.</span><span class="sxs-lookup"><span data-stu-id="254db-113">**Azure Custom Vision** is part of the **Cognitive Services** family and is used to train image classifiers.</span></span> <span data-ttu-id="254db-114">Le classifieur d’images est un service IA qui utilise le modèle entraîné pour appliquer des étiquettes correspondantes.</span><span class="sxs-lookup"><span data-stu-id="254db-114">The image classifier is an AI service that uses the trained model to apply matching tags.</span></span> <span data-ttu-id="254db-115">Cette fonctionnalité de classification sera utilisée par notre application pour détecter les *objets suivis*.</span><span class="sxs-lookup"><span data-stu-id="254db-115">This classification feature will be used by our application to detect *Tracked Objects*.</span></span>

<span data-ttu-id="254db-116">Apprenez-en davantage sur [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span><span class="sxs-lookup"><span data-stu-id="254db-116">Learn more about [Azure Custom Vision](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span></span>

## <a name="preparing-azure-custom-vision"></a><span data-ttu-id="254db-117">Préparation d’Azure Custom Vision</span><span class="sxs-lookup"><span data-stu-id="254db-117">Preparing Azure Custom Vision</span></span>

<span data-ttu-id="254db-118">Avant de commencer, vous devez créer un projet Custom Vision ; le moyen le plus rapide consiste à utiliser le portail web.</span><span class="sxs-lookup"><span data-stu-id="254db-118">Before you can start, you have to create a custom vision project, the fastest way is by using the web portal.</span></span>

<span data-ttu-id="254db-119">Suivez ce [tutoriel de démarrage rapide](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier#choose-training-images) pour configurer votre compte et votre projet jusqu’à la section *Charger et étiqueter des images*.</span><span class="sxs-lookup"><span data-stu-id="254db-119">Follow this [quickstart tutorial](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/getting-started-build-a-classifier#choose-training-images) to setup your account and project until section *Upload and tag images*.</span></span>

> [!WARNING]
> <span data-ttu-id="254db-120">Pour entraîner un modèle, vous devez avoir au moins deux étiquettes et cinq images par étiquette.</span><span class="sxs-lookup"><span data-stu-id="254db-120">To train a model you need to have at least 2 tags and 5 images per tag.</span></span> <span data-ttu-id="254db-121">Pour utiliser cette application, vous devez créer au moins une étiquette avec cinq images, afin que le processus d’entraînement n’échoue pas par la suite.</span><span class="sxs-lookup"><span data-stu-id="254db-121">To use this application you should at least create one tag with 5 images, so that the training process later won't fail.</span></span>

## <a name="preparing-the-scene"></a><span data-ttu-id="254db-122">Préparation de la scène</span><span class="sxs-lookup"><span data-stu-id="254db-122">Preparing the scene</span></span>

<span data-ttu-id="254db-123">Dans la fenêtre Project, accédez au dossier **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager**.</span><span class="sxs-lookup"><span data-stu-id="254db-123">In the Project window, navigate to the **Assets** > **MRTK.Tutorials.AzureCloudServices** > **Prefabs** > **Manager** folder.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial3-section4-step1-1.png)

<span data-ttu-id="254db-125">À partir de là, faites glisser le préfabriqué **ObjectDetectionManager** dans la hiérarchie de la scène.</span><span class="sxs-lookup"><span data-stu-id="254db-125">From there drag the prefab **ObjectDetectionManager** into the scene Hierarchy.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial3-section4-step1-2.png)

<span data-ttu-id="254db-127">Dans la fenêtre de hiérarchie, recherchez l’objet **ObjectDetectionManager** et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="254db-127">In the Hierarchy window locate the **ObjectDetectionManager** object and select it.</span></span>
<span data-ttu-id="254db-128">Le préfabriqué **ObjectDetectionManager** contient le composant **ObjectDetectionManager (script)** et, comme vous pouvez le voir dans la fenêtre de l’inspecteur, il dépend de plusieurs paramètres.</span><span class="sxs-lookup"><span data-stu-id="254db-128">The **ObjectDetectionManager** prefab contains the **ObjectDetectionManager (script)** component and as you can see from the Inspector window it depends on several settings.</span></span>

## <a name="retrieving-azure-api-resource-credentials"></a><span data-ttu-id="254db-129">Récupération des informations d’identification de la ressource API Azure</span><span class="sxs-lookup"><span data-stu-id="254db-129">Retrieving Azure api resource credentials</span></span>

<span data-ttu-id="254db-130">Les informations d’identification nécessaires pour les paramètres d’**ObjectDetectionManager (script)** peuvent être récupérées à partir du portail Azure et du portail Custom Vision.</span><span class="sxs-lookup"><span data-stu-id="254db-130">The necessary credentials for the **ObjectDetectionManager (script)** settings can be retrieve from the Azure Portal and the custom vision portal.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="254db-131">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="254db-131">Azure Portal</span></span>

<span data-ttu-id="254db-132">Recherchez la ressource Custom Vision de type **Cognitive Services** que vous avez créée dans la section *Préparation de la scène* de ce tutoriel.</span><span class="sxs-lookup"><span data-stu-id="254db-132">Find and locate the custom vision resource of type **Cognitive Services** you have created in the *Preparing the scene* section of this tutorial.</span></span> <span data-ttu-id="254db-133">Cliquez sur *Clés et point de terminaison* pour récupérer les informations d’identification nécessaires.</span><span class="sxs-lookup"><span data-stu-id="254db-133">There click on *Keys and Endpoint* to retrieve the necessary credentials.</span></span>

### <a name="custom-vision-dashboard"></a><span data-ttu-id="254db-134">Tableau de bord Custom Vision</span><span class="sxs-lookup"><span data-stu-id="254db-134">Custom Vision Dashboard</span></span>

<span data-ttu-id="254db-135">Dans le tableau de bord [Custom Vision](https://www.customvision.ai/projects), ouvrez le projet que vous avez créé pour ce tutoriel, puis cliquez en haut à droite de la page sur l’icône d’engrenage pour ouvrir la page Paramètres.</span><span class="sxs-lookup"><span data-stu-id="254db-135">In the [custom vision](https://www.customvision.ai/projects) dashboard, open the project you have created for this tutorial and click on the top right corner of the page on the gear icon to open the settings page.</span></span> <span data-ttu-id="254db-136">Dans la section de droite *Resources*, vous trouverez les informations d’identification nécessaires.</span><span class="sxs-lookup"><span data-stu-id="254db-136">Here on the right hand *Resources* section you will find the necessary credentials.</span></span>

<span data-ttu-id="254db-137">Le composant **ObjectDetectionManager (script)** étant maintenant configuré correctement, recherchez l’objet **SceneController** dans la hiérarchie de la scène et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="254db-137">Now with the **ObjectDetectionManager (script)** setup correctly, find the **SceneController** object in your scene Hierarchy and select it.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial3-section4-step1-3.png)

<span data-ttu-id="254db-139">Vous constatez que le champ *Object Detection Manager* (Gestionnaire de détection d’objets) dans le composant **SceneController** est vide. Faites glisser l’**ObjectDetectionManager** de la hiérarchie vers ce champ et enregistrez la scène.</span><span class="sxs-lookup"><span data-stu-id="254db-139">You see *Object Detection Manager* field in the **SceneController** component is empty, drag the **ObjectDetectionManager** from the Hierarchy into that field and save the scene.</span></span>

![mr-learning-azure](images/mr-learning-azure/tutorial3-section4-step1-4.png)

## <a name="take-and-upload-images"></a><span data-ttu-id="254db-141">Capturer et charger des images</span><span class="sxs-lookup"><span data-stu-id="254db-141">Take and upload images</span></span>

<span data-ttu-id="254db-142">Exécutez la scène, cliquez sur **Set Object** (Définir l’objet), puis tapez le nom de l’un des **objets suivis** que vous avez créés dans la [leçon précédente](mr-learning-azure-02.md).</span><span class="sxs-lookup"><span data-stu-id="254db-142">Run the scene and click on **Set Object**, type in the name for one of the **Tracked Objects** you have created in the [previous lesson](mr-learning-azure-02.md).</span></span> <span data-ttu-id="254db-143">Cliquez à présent sur le bouton **Computer Vision** qui figure en bas de la **fiche d’objet**.</span><span class="sxs-lookup"><span data-stu-id="254db-143">Now click on **Computer Vision** button you can find at the bottom of the **Object Card**.</span></span>

<span data-ttu-id="254db-144">Une nouvelle fenêtre s’ouvre, dans laquelle vous devez prendre six photos pour entraîner le modèle à la reconnaissance d’image.</span><span class="sxs-lookup"><span data-stu-id="254db-144">A new window will open where you have to take six photos to train the model for image recognition.</span></span> <span data-ttu-id="254db-145">Cliquez sur le bouton **Camera** et effectuez un clic aérien lorsque vous regardez l’objet que vous voulez suivre. Répétez cette opération à six reprises.</span><span class="sxs-lookup"><span data-stu-id="254db-145">Click on the **Camera** button and perform an AirTap when you look on the object you like to track, do this six times.</span></span>

> [!TIP]
> <span data-ttu-id="254db-146">Pour améliorer l’entraînement du modèle, essayez de capturer chaque image à partir de différents angles et conditions d’éclairage.</span><span class="sxs-lookup"><span data-stu-id="254db-146">To improve the model training try to take each image from different angles and lighting conditions.</span></span>

<span data-ttu-id="254db-147">Une fois que vous avez suffisamment d’images, cliquez sur le bouton **Train** (Entraîner) pour démarrer le processus d’entraînement du modèle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="254db-147">Once you have enough images click on the **Train** button to start the model training process in the cloud.</span></span> <span data-ttu-id="254db-148">L’activation de l’entraînement provoque le chargement de toutes les images, puis le démarrage de l’entraînement. Cette opération peut prendre jusqu’à une minute, voire plus.</span><span class="sxs-lookup"><span data-stu-id="254db-148">Activating the training will upload all images and then start the training, this can take up to a minute or more.</span></span> <span data-ttu-id="254db-149">Un message à l’intérieur du menu indique la progression actuelle et, une fois qu’il indique que l’opération est terminée, vous pouvez arrêter l’application.</span><span class="sxs-lookup"><span data-stu-id="254db-149">A message inside the menu indicates the current progress and once it indicates the completion you can stop the application</span></span>

> [!TIP]
> <span data-ttu-id="254db-150">Le composant **ObjectDetectionManager (script)** charge directement les images prises dans le service Custom Vision.</span><span class="sxs-lookup"><span data-stu-id="254db-150">The **ObjectDetectionManager (script)** directly uploads taken images into the Custom Vision service.</span></span> <span data-ttu-id="254db-151">En guise d’alternative, l’API Custom Vision accepte les URL vers les images. Comme exercice, vous pouvez modifier l’**ObjectDetectionManager (script)** afin qu’il charge plutôt les images dans un stockage Blob.</span><span class="sxs-lookup"><span data-stu-id="254db-151">As an alternative the custom vision API accepts URLs to the images, as an exercise you can modify the **ObjectDetectionManager (script)** to upload the images to a Blob storage instead.</span></span>

## <a name="detect-objects"></a><span data-ttu-id="254db-152">Détecter des objets</span><span class="sxs-lookup"><span data-stu-id="254db-152">Detect objects</span></span>

<span data-ttu-id="254db-153">Vous pouvez maintenant tester le modèle entraîné. Exécutez l’application et, dans le *menu principal*, cliquez sur **Search Object** (Rechercher un objet) et tapez le nom de l’**objet suivi** en question.</span><span class="sxs-lookup"><span data-stu-id="254db-153">You can now put the trained model to the test, run the application and from the *main menu* click on **Search Object** and type the name of the **Tracked Object** in question.</span></span> <span data-ttu-id="254db-154">La **fiche d’objet** apparaît. Cliquez sur le bouton **Custom Vision**.</span><span class="sxs-lookup"><span data-stu-id="254db-154">The **Object Card** will appear and click on the **Custom Vision** button.</span></span> <span data-ttu-id="254db-155">À partir de là, le composant **ObjectDetectionManager** commence à effectuer des captures d’images en arrière-plan à partir de l’appareil photo, et la progression sera indiquée dans le menu.</span><span class="sxs-lookup"><span data-stu-id="254db-155">From here the **ObjectDetectionManager** will start taking image captures in the background from the camera and the progress will be indicated on the menu.</span></span> <span data-ttu-id="254db-156">Pointez l’appareil photo sur l’objet que vous avez utilisé pour l’entraînement du modèle, et vous constaterez qu’après quelques instants il détectera l’objet.</span><span class="sxs-lookup"><span data-stu-id="254db-156">Point the camera to the object you used to train the model and you will see that after a short while it will detect the object.</span></span>

## <a name="congratulations"></a><span data-ttu-id="254db-157">Félicitations</span><span class="sxs-lookup"><span data-stu-id="254db-157">Congratulations</span></span>

<span data-ttu-id="254db-158">Dans ce tutoriel, vous avez appris à utiliser Azure Custom Vision pour entraîner des images et utiliser le service de classification pour détecter les images qui correspondent à l’**objet suivi** associé.</span><span class="sxs-lookup"><span data-stu-id="254db-158">In this tutorial you learned how Azure Custom Vision can be used to train images and use the classification service to detect images that match the associated **Tracked Object**.</span></span>

<span data-ttu-id="254db-159">Dans le tutoriel suivant, vous allez apprendre à utiliser Azure Spatial Anchors pour lier un *objet suivi* à un emplacement dans le monde physique, puis à afficher une flèche qui guidera l’utilisateur vers l’emplacement lié de l’objet suivi.</span><span class="sxs-lookup"><span data-stu-id="254db-159">In the next tutorial you will learn how to use Azure Spatial Anchors to link a *Tracked Object* with a location in the physical world and how to display an arrow that will guide the user back to the Tracked Object's linked location.</span></span>

[<span data-ttu-id="254db-160">Tutoriel suivant : 4. Intégration d’Azure Spatial Anchors</span><span class="sxs-lookup"><span data-stu-id="254db-160">Next tutorial: 4. Integrating Azure Spatial Anchors</span></span>](mr-learning-azure-04.md)
