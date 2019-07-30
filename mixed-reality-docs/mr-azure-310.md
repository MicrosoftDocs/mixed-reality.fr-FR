---
title: MR et Azure 310-détection d’objets
description: Suivez ce cours pour apprendre à former un modèle de Machine Learning, puis à utiliser le modèle formé pour reconnaître des objets similaires et leur position dans le monde réel à partir d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, vision personnalisée, détection d’objets, réalité mixte, Académie, Unity, didacticiel, API, hololens
ms.openlocfilehash: 89ee79943a88de8a34c679ae33621db5770908b0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63544458"
---
>[!NOTE]
><span data-ttu-id="242b4-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="242b4-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="242b4-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="242b4-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="242b4-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="242b4-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="242b4-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="242b4-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="242b4-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="242b4-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="242b4-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="242b4-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-310-object-detection"></a><span data-ttu-id="242b4-110">Mr et Azure 310: Détection d’objet</span><span class="sxs-lookup"><span data-stu-id="242b4-110">Mr and Azure 310: Object detection</span></span>

<span data-ttu-id="242b4-111">Dans ce cours, vous allez apprendre à reconnaître le contenu visuel personnalisé et sa position spatiale dans une image fournie, en utilisant les fonctionnalités de «détection d’objets» d’Azure Custom Vision dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="242b4-111">In this course, you will learn how to recognize custom visual content and its spatial position within a provided image, using Azure Custom Vision "Object Detection" capabilities in a mixed reality application.</span></span>

<span data-ttu-id="242b4-112">Ce service vous permet d’effectuer l’apprentissage d’un modèle de Machine Learning à l’aide d’images d’objet.</span><span class="sxs-lookup"><span data-stu-id="242b4-112">This service will allow you to train a machine learning model using object images.</span></span> <span data-ttu-id="242b4-113">Vous allez ensuite utiliser le modèle formé pour reconnaître des objets similaires et se rapprocher de leur emplacement dans le monde réel, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou d’une caméra qui se connecte à un PC pour les casques immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="242b4-113">You will then use the trained model to recognize similar objects and approximate their location in the real world, as provided by the camera capture of Microsoft HoloLens or a camera connect to a PC for immersive (VR) headsets.</span></span>

![résultat du cours](images/AzureLabs-Lab310-00.png)

<span data-ttu-id="242b4-115">**Azure Custom vision, la détection d’objets** est un service Microsoft qui permet aux développeurs de créer des classifieurs d’images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="242b4-115">**Azure Custom Vision, Object Detection** is a Microsoft Service which allows developers to build custom image classifiers.</span></span> <span data-ttu-id="242b4-116">Ces classifieurs peuvent ensuite être utilisés avec de nouvelles images pour détecter des objets dans cette nouvelle image, en fournissant des **limites de zone** au sein de l’image elle-même.</span><span class="sxs-lookup"><span data-stu-id="242b4-116">These classifiers can then be used with new images to detect objects within that new image, by providing **Box Boundaries** within the image itself.</span></span> <span data-ttu-id="242b4-117">Le service fournit un portail en ligne simple et facile à utiliser pour simplifier ce processus.</span><span class="sxs-lookup"><span data-stu-id="242b4-117">The Service provides a simple, easy to use, online portal to streamline this process.</span></span> <span data-ttu-id="242b4-118">Pour plus d’informations, consultez les liens suivants:</span><span class="sxs-lookup"><span data-stu-id="242b4-118">For more information, visit the following links:</span></span>

* [<span data-ttu-id="242b4-119">Page Custom Vision Azure</span><span class="sxs-lookup"><span data-stu-id="242b4-119">Azure Custom Vision page</span></span>](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home)
* [<span data-ttu-id="242b4-120">Limites et quotas</span><span class="sxs-lookup"><span data-stu-id="242b4-120">Limits and Quotas</span></span>](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/limits-and-quotas)

<span data-ttu-id="242b4-121">À la fin de ce cours, vous disposerez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-121">Upon completion of this course, you will have a mixed reality application which will be able to do the following:</span></span>

1. <span data-ttu-id="242b4-122">L’utilisateur sera en *mesure de* pointer vers un objet, qu’il a formé à l’aide du service vision personnalisée Azure, détection d’objet.</span><span class="sxs-lookup"><span data-stu-id="242b4-122">The user will be able to *gaze* at an object, which they have trained using the Azure Custom Vision Service, Object Detection.</span></span> 
2. <span data-ttu-id="242b4-123">L’utilisateur utilise le geste *Tap* pour capturer une image de ce qu’il examine.</span><span class="sxs-lookup"><span data-stu-id="242b4-123">The user will use the *Tap* gesture to capture an image of what they are looking at.</span></span>
3. <span data-ttu-id="242b4-124">L’application enverra l’image à la Service Vision personnalisée Azure.</span><span class="sxs-lookup"><span data-stu-id="242b4-124">The app will send the image to the Azure Custom Vision Service.</span></span>
4. <span data-ttu-id="242b4-125">Il y aura une réponse du service qui affichera le résultat de la reconnaissance sous forme de texte d’espace universel.</span><span class="sxs-lookup"><span data-stu-id="242b4-125">There will be a reply from the Service which will display the result of the recognition as world-space text.</span></span> <span data-ttu-id="242b4-126">Pour ce faire, vous devez utiliser le suivi spatial de Microsoft HoloLens, afin de comprendre la position universelle de l’objet reconnu, puis l’utilisation de la *balise* associée à ce qui est détecté dans l’image, pour fournir le texte de l’étiquette.</span><span class="sxs-lookup"><span data-stu-id="242b4-126">This will be accomplished through utilizing the Microsoft HoloLens' Spatial Tracking, as a way of understanding the world position of the recognized object, and then using the *Tag* associated with what is detected in the image, to provide the label text.</span></span>

<span data-ttu-id="242b4-127">Ce cours couvre également le chargement manuel d’images, la création de balises et l’apprentissage du service, pour reconnaître différents objets (dans l’exemple fourni, une tasse), en définissant la *zone limite* dans l’image que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="242b4-127">The course will also cover manually uploading images, creating tags, and training the Service, to recognize different objects (in the provided example, a cup), by setting the *Boundary Box* within the image you submit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="242b4-128">Après la création et l’utilisation de l’application, le développeur doit revenir à la Service Vision personnalisée Azure, identifier les prédictions effectuées par le service et déterminer si elles sont correctes ou non (en marquant tout ce que le service a manqué) et réglage des *zones englobantes*).</span><span class="sxs-lookup"><span data-stu-id="242b4-128">Following the creation and use of the app, the developer should navigate back to the Azure Custom Vision Service, and identify the predictions made by the Service, and determine whether they were correct or not (through tagging anything the Service missed, and adjusting the *Bounding Boxes*).</span></span> <span data-ttu-id="242b4-129">Le service peut ensuite être réformé, ce qui augmente la probabilité qu’il reconnaisse les objets réels.</span><span class="sxs-lookup"><span data-stu-id="242b4-129">The Service can then be re-trained, which will increase the likelihood of it recognizing real world objects.</span></span>

<span data-ttu-id="242b4-130">Ce cours vous apprend à obtenir les résultats de la Service Vision personnalisée Azure, la détection d’objets, dans un exemple d’application à base d’Unity.</span><span class="sxs-lookup"><span data-stu-id="242b4-130">This course will teach you how to get the results from the Azure Custom Vision Service, Object Detection, into a Unity-based sample application.</span></span> <span data-ttu-id="242b4-131">Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.</span><span class="sxs-lookup"><span data-stu-id="242b4-131">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="242b4-132">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="242b4-132">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="242b4-133">Course</span><span class="sxs-lookup"><span data-stu-id="242b4-133">Course</span></span></th><th style="width:150px"> <span data-ttu-id="242b4-134"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="242b4-134"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="242b4-135"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="242b4-135"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="242b4-136">MR et Azure 310: Détection d’objet</span><span class="sxs-lookup"><span data-stu-id="242b4-136">MR and Azure 310: Object detection</span></span></td><td style="text-align: center;"> <span data-ttu-id="242b4-137">✔️</span><span class="sxs-lookup"><span data-stu-id="242b4-137">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="242b4-138">Prérequis</span><span class="sxs-lookup"><span data-stu-id="242b4-138">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="242b4-139">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="242b4-139">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="242b4-140">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="242b4-140">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="242b4-141">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="242b4-141">You are free to use the latest software, as listed within the [install the tools](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="242b4-142">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="242b4-142">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="242b4-143">Un PC de développement</span><span class="sxs-lookup"><span data-stu-id="242b4-143">A development PC</span></span>
- [<span data-ttu-id="242b4-144">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="242b4-144">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="242b4-145">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="242b4-145">The latest Windows 10 SDK</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="242b4-146">Unity 2017,4 LTS</span><span class="sxs-lookup"><span data-stu-id="242b4-146">Unity 2017.4 LTS</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="242b4-147">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="242b4-147">Visual Studio 2017</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- <span data-ttu-id="242b4-148">[Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) avec mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="242b4-148">A [Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) with Developer mode enabled</span></span>
- <span data-ttu-id="242b4-149">Accès à Internet pour l’installation d’Azure et la récupération de Service Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="242b4-149">Internet access for Azure setup and Custom Vision Service retrieval</span></span>
-  <span data-ttu-id="242b4-150">Une série d’au moins quinze (15) images sont requises) pour chaque objet que vous souhaitez que le Custom Vision reconnaître.</span><span class="sxs-lookup"><span data-stu-id="242b4-150">A series of at least fifteen (15) images are required) for each object that you would like the Custom Vision to recognize.</span></span> <span data-ttu-id="242b4-151">Si vous le souhaitez, vous pouvez utiliser les images déjà fournies dans ce cours, [une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span><span class="sxs-lookup"><span data-stu-id="242b4-151">If you wish, you can use the images already provided with this course, [a series of cups](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="242b4-152">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="242b4-152">Before you start</span></span>

1.  <span data-ttu-id="242b4-153">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="242b4-153">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="242b4-154">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="242b4-154">Set up and test your HoloLens.</span></span> <span data-ttu-id="242b4-155">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="242b4-155">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="242b4-156">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="242b4-156">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="242b4-157">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="242b4-157">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="242b4-158">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="242b4-158">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-custom-vision-portal"></a><span data-ttu-id="242b4-159">Chapitre 1-portail Custom Vision</span><span class="sxs-lookup"><span data-stu-id="242b4-159">Chapter 1 - The Custom Vision Portal</span></span>

<span data-ttu-id="242b4-160">Pour utiliser le **service vision personnalisée Azure**, vous devez configurer une instance de ce dernier pour qu’il soit mis à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="242b4-160">To use the **Azure Custom Vision Service**, you will need to configure an instance of it to be made available to your application.</span></span>

1.  <span data-ttu-id="242b4-161">Accédez [à la page principale de **service vision personnalisée** ](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span><span class="sxs-lookup"><span data-stu-id="242b4-161">Navigate [to the **Custom Vision Service** main page](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span></span>

2.  <span data-ttu-id="242b4-162">Cliquez sur **prise en main**.</span><span class="sxs-lookup"><span data-stu-id="242b4-162">Click on **Getting Started**.</span></span>

    ![](images/AzureLabs-Lab310-01.png)

3.  <span data-ttu-id="242b4-163">Connectez-vous au portail Custom Vision.</span><span class="sxs-lookup"><span data-stu-id="242b4-163">Sign in to the Custom Vision Portal.</span></span>

    ![](images/AzureLabs-Lab310-02.png)

4.  <span data-ttu-id="242b4-164">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="242b4-164">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="242b4-165">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="242b4-165">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

5.  <span data-ttu-id="242b4-166">Une fois que vous êtes connecté pour la première fois, vous êtes invité à entrer dans le panneau *des conditions d’accès* .</span><span class="sxs-lookup"><span data-stu-id="242b4-166">Once you are logged in for the first time, you will be prompted with the *Terms of Service* panel.</span></span> <span data-ttu-id="242b4-167">Cochez la case pour *accepter les termes du contrat*.</span><span class="sxs-lookup"><span data-stu-id="242b4-167">Click the checkbox to *agree to the terms*.</span></span> <span data-ttu-id="242b4-168">Cliquez ensuite sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="242b4-168">Then click **I agree**.</span></span>

    ![](images/AzureLabs-Lab310-03.png)

6.  <span data-ttu-id="242b4-169">Après avoir accepté les termes, vous vous trouvez maintenant dans la section *mes projets* .</span><span class="sxs-lookup"><span data-stu-id="242b4-169">Having agreed to the terms, you are now in the *My Projects* section.</span></span> <span data-ttu-id="242b4-170">Cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="242b4-170">Click on **New Project**.</span></span>

    ![](images/AzureLabs-Lab310-04.png)

7.  <span data-ttu-id="242b4-171">Un onglet s’affiche sur le côté droit, ce qui vous invite à spécifier certains champs pour le projet.</span><span class="sxs-lookup"><span data-stu-id="242b4-171">A tab will appear on the right-hand side, which will prompt you to specify some fields for the project.</span></span>

    1.  <span data-ttu-id="242b4-172">Insérer un nom pour votre projet</span><span class="sxs-lookup"><span data-stu-id="242b4-172">Insert a name for your project</span></span>

    2.  <span data-ttu-id="242b4-173">Insérer une description pour votre projet (**facultatif**)</span><span class="sxs-lookup"><span data-stu-id="242b4-173">Insert a description for your project (**Optional**)</span></span>

    3.  <span data-ttu-id="242b4-174">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="242b4-174">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="242b4-175">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="242b4-175">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="242b4-176">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="242b4-176">It is recommended to keep all the Azure services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        ![](images/AzureLabs-Lab310-05.png)

        > [!NOTE]
        > <span data-ttu-id="242b4-177">Si vous souhaitez [en savoir plus sur les groupes de ressources Azure, accédez aux documents associés](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal) .</span><span class="sxs-lookup"><span data-stu-id="242b4-177">If you wish to [read more about Azure Resource Groups, navigate to the associated Docs](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span></span>

    4.  <span data-ttu-id="242b4-178">Définissez les **types de projets** en tant que **détection d’objet (** préversion).</span><span class="sxs-lookup"><span data-stu-id="242b4-178">Set the **Project Types** as **Object Detection (preview)**.</span></span>

8.  <span data-ttu-id="242b4-179">Une fois que vous avez terminé, cliquez sur **créer un projet**. vous êtes alors redirigé vers la page du projet service vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="242b4-179">Once you are finished, click on **Create project**, and you will be redirected to the Custom Vision Service project page.</span></span>


## <a name="chapter-2---training-your-custom-vision-project"></a><span data-ttu-id="242b4-180">Chapitre 2-formation de votre projet Custom Vision</span><span class="sxs-lookup"><span data-stu-id="242b4-180">Chapter 2 - Training your Custom Vision project</span></span>

<span data-ttu-id="242b4-181">Une fois dans le portail Custom Vision, votre objectif principal est de former votre projet à la reconnaissance d’objets spécifiques dans les images.</span><span class="sxs-lookup"><span data-stu-id="242b4-181">Once in the Custom Vision Portal, your primary objective is to train your project to recognize specific objects in images.</span></span>

<span data-ttu-id="242b4-182">Vous avez besoin d’au moins quinze (15) images pour chaque objet que vous souhaitez que votre application reconnaisse.</span><span class="sxs-lookup"><span data-stu-id="242b4-182">You need at least fifteen (15) images for each object that you would like your application to recognize.</span></span> <span data-ttu-id="242b4-183">Vous pouvez utiliser les images fournies avec ce cours ([une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span><span class="sxs-lookup"><span data-stu-id="242b4-183">You can use the images provided with this course ([a series of cups](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span></span>

<span data-ttu-id="242b4-184">Pour former votre projet Custom Vision:</span><span class="sxs-lookup"><span data-stu-id="242b4-184">To train your Custom Vision project:</span></span>

1.  <span data-ttu-id="242b4-185">Cliquez sur le **+** bouton en regardde balises.</span><span class="sxs-lookup"><span data-stu-id="242b4-185">Click on the **+** button next to **Tags**.</span></span>

    ![](images/AzureLabs-Lab310-06.png)

2.  <span data-ttu-id="242b4-186">Ajoutez un **nom** pour la balise qui sera utilisée pour associer vos images à.</span><span class="sxs-lookup"><span data-stu-id="242b4-186">Add a **name** for the tag that will be used to associate your images with.</span></span> <span data-ttu-id="242b4-187">Dans cet exemple, nous utilisons des images de tasses pour la reconnaissance, vous avez donc nommé la balise pour This, **Cup**.</span><span class="sxs-lookup"><span data-stu-id="242b4-187">In this example we are using images of cups for recognition, so have named the tag for this, **Cup**.</span></span> <span data-ttu-id="242b4-188">Cliquez sur **Enregistrer** une fois l’opération terminée.</span><span class="sxs-lookup"><span data-stu-id="242b4-188">Click **Save** once finished.</span></span>

    ![](images/AzureLabs-Lab310-07.png)

3.  <span data-ttu-id="242b4-189">Vous remarquerez que votre balise a été ajoutée (vous devrez peut-être recharger votre page pour qu’elle apparaisse).</span><span class="sxs-lookup"><span data-stu-id="242b4-189">You will notice your **Tag** has been added (you may need to reload your page for it to appear).</span></span> 

    ![](images/AzureLabs-Lab310-08.png)

4.  <span data-ttu-id="242b4-190">Cliquez sur **Ajouter des images** au centre de la page.</span><span class="sxs-lookup"><span data-stu-id="242b4-190">Click on **Add images** in the center of the page.</span></span>

    ![](images/AzureLabs-Lab310-09.png)

5.  <span data-ttu-id="242b4-191">Cliquez sur **Parcourir les fichiers locaux**et recherchez les images que vous souhaitez télécharger pour un objet, avec un minimum de 15 (15).</span><span class="sxs-lookup"><span data-stu-id="242b4-191">Click on **Browse local files**, and browse to the images you would like to upload for one object, with the minimum being fifteen (15).</span></span>

    > [!TIP]
    >  <span data-ttu-id="242b4-192">Vous pouvez sélectionner plusieurs images à la fois, à télécharger.</span><span class="sxs-lookup"><span data-stu-id="242b4-192">You can select several images at a time, to upload.</span></span>

    ![](images/AzureLabs-Lab310-10.png)

6.  <span data-ttu-id="242b4-193">Appuyez sur **charger les fichiers** une fois que vous avez sélectionné toutes les images avec lesquelles vous souhaitez former le projet.</span><span class="sxs-lookup"><span data-stu-id="242b4-193">Press **Upload files** once you have selected all the images you would like to train the project with.</span></span> <span data-ttu-id="242b4-194">Le chargement des fichiers va commencer.</span><span class="sxs-lookup"><span data-stu-id="242b4-194">The files will begin uploading.</span></span> <span data-ttu-id="242b4-195">Une fois que vous avez confirmé le téléchargement, cliquez sur **terminé**.</span><span class="sxs-lookup"><span data-stu-id="242b4-195">Once you have confirmation of the upload, click **Done**.</span></span>

    ![](images/AzureLabs-Lab310-11.png)

7.  <span data-ttu-id="242b4-196">À ce stade, vos images sont chargées, mais elles ne sont pas marquées.</span><span class="sxs-lookup"><span data-stu-id="242b4-196">At this point your images are uploaded, but not tagged.</span></span>

    ![](images/AzureLabs-Lab310-12.png)

8.  <span data-ttu-id="242b4-197">Pour baliser vos images, utilisez la souris.</span><span class="sxs-lookup"><span data-stu-id="242b4-197">To tag your images, use your mouse.</span></span> <span data-ttu-id="242b4-198">Au fur et à mesure que vous pointez sur votre image, une sélection de sélection vous aidera en dessinant automatiquement une sélection autour de votre objet.</span><span class="sxs-lookup"><span data-stu-id="242b4-198">As you hover over your image, a selection highlight will aid you by automatically drawing a selection around your object.</span></span> <span data-ttu-id="242b4-199">Si ce n’est pas exact, vous pouvez créer les vôtres.</span><span class="sxs-lookup"><span data-stu-id="242b4-199">If it is not accurate, you can draw your own.</span></span> <span data-ttu-id="242b4-200">Pour ce faire, vous devez maintenir le bouton gauche de la souris enfoncé et faire glisser la région de sélection pour englober votre objet.</span><span class="sxs-lookup"><span data-stu-id="242b4-200">This is accomplished by holding left-click on the mouse, and dragging the selection region to encompass your object.</span></span> 

    ![](images/AzureLabs-Lab310-13.png) 

9. <span data-ttu-id="242b4-201">Après la sélection de votre objet dans l’image, une petite invite vous demande d’ajouter une *balise de région*.</span><span class="sxs-lookup"><span data-stu-id="242b4-201">Following the selection of your object within the image, a small prompt will ask for you to *Add Region Tag*.</span></span> <span data-ttu-id="242b4-202">Sélectionnez votre balise créée précédemment («Cup», dans l’exemple ci-dessus), ou si vous ajoutez d’autres balises, tapez ce qui se trouve dans et cliquez sur le bouton **+ (plus)** .</span><span class="sxs-lookup"><span data-stu-id="242b4-202">Select your previously created tag ('Cup', in the above example), or if you are adding more tags, type that in and click the **+ (plus)** button.</span></span>

    ![](images/AzureLabs-Lab310-14.png) 

10. <span data-ttu-id="242b4-203">Pour baliser l’image suivante, vous pouvez cliquer sur la flèche à droite du panneau ou fermer le panneau des balises (en cliquant sur le **X** dans le coin supérieur droit du panneau), puis sur l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="242b4-203">To tag the next image, you can click the arrow to the right of the blade, or close the tag blade (by clicking the **X** in the top-right corner of the blade) and then click the next image.</span></span> <span data-ttu-id="242b4-204">Une fois que l’image suivante est prête, répétez la même procédure.</span><span class="sxs-lookup"><span data-stu-id="242b4-204">Once you have the next image ready, repeat the same procedure.</span></span> <span data-ttu-id="242b4-205">Procédez ainsi pour toutes les images que vous avez chargées, jusqu’à ce qu’elles soient toutes marquées.</span><span class="sxs-lookup"><span data-stu-id="242b4-205">Do this for all the images you have uploaded, until they are all tagged.</span></span> 

    > [!NOTE]
    >  <span data-ttu-id="242b4-206">Vous pouvez sélectionner plusieurs objets dans la même image, comme l’image ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="242b4-206">You can select several objects in the same image, like the image below:</span></span> 
    > 
    > ![](images/AzureLabs-Lab310-15.png)

11. <span data-ttu-id="242b4-207">Une fois que vous les avez balisées, cliquez sur le bouton **balisé** , à gauche de l’écran, pour afficher les images avec balises.</span><span class="sxs-lookup"><span data-stu-id="242b4-207">Once you have tagged them all, click on the **tagged** button, on the left of the screen, to reveal the tagged images.</span></span> 

    ![](images/AzureLabs-Lab310-16.png)

12. <span data-ttu-id="242b4-208">Vous êtes maintenant prêt à former votre service.</span><span class="sxs-lookup"><span data-stu-id="242b4-208">You are now ready to train your Service.</span></span> <span data-ttu-id="242b4-209">Cliquez sur le bouton **former** et la première itération d’apprentissage commencera.</span><span class="sxs-lookup"><span data-stu-id="242b4-209">Click the **Train** button, and the first training iteration will begin.</span></span>

    ![](images/AzureLabs-Lab310-17.png)

    ![](images/AzureLabs-Lab310-18.png)

13. <span data-ttu-id="242b4-210">Une fois qu’elle est créée, vous pouvez voir deux boutons nommés **créer par défaut** et **URL**de prédiction.</span><span class="sxs-lookup"><span data-stu-id="242b4-210">Once it is built, you will be able to see two buttons called **Make default** and **Prediction URL**.</span></span> <span data-ttu-id="242b4-211">Cliquez d’abord sur **créer par défaut** , puis sur **URL**de prédiction.</span><span class="sxs-lookup"><span data-stu-id="242b4-211">Click on **Make default** first, then click on **Prediction URL**.</span></span>

    ![](images/AzureLabs-Lab310-19.png)

    > [!NOTE] 
    > <span data-ttu-id="242b4-212">Le point de terminaison fourni à partir de ce est défini sur l' *itération* qui a été marquée comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="242b4-212">The endpoint which is provided from this, is set to whichever *Iteration* has been marked as default.</span></span> <span data-ttu-id="242b4-213">Par conséquent, si vous effectuez ultérieurement une nouvelle *itération* et la mettez à jour par défaut, vous n’aurez pas besoin de modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="242b4-213">As such, if you later make a new *Iteration* and update it as default, you will not need to change your code.</span></span>

14. <span data-ttu-id="242b4-214">Une fois que vous avez cliqué **sur URL**de prédiction, ouvrez le *bloc-notes*, puis copiez et collez l' **URL** (également appelée « **prédiction-point de terminaison»** ) et la **clé de prédiction de service**, afin de pouvoir la récupérer lorsque vous en aurez besoin ultérieurement dans le code.</span><span class="sxs-lookup"><span data-stu-id="242b4-214">Once you have clicked on **Prediction URL**, open *Notepad*, and copy and paste the **URL** (also called your **Prediction-Endpoint**) and the **Service Prediction-Key**, so that you can retrieve it when you need it later in the code.</span></span>

    ![](images/AzureLabs-Lab310-20.png)

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="242b4-215">Chapitre 3-configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="242b4-215">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="242b4-216">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="242b4-216">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="242b4-217">Ouvrez **Unity** et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="242b4-217">Open **Unity** and click **New**.</span></span>

    ![](images/AzureLabs-Lab310-21.png)

2.  <span data-ttu-id="242b4-218">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="242b4-218">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="242b4-219">Insérez **CustomVisionObjDetection**.</span><span class="sxs-lookup"><span data-stu-id="242b4-219">Insert **CustomVisionObjDetection**.</span></span> <span data-ttu-id="242b4-220">Assurez-vous que le type de projet est défini sur **3D**et définissez l’emplacement sur un **emplacement** approprié (n’oubliez pas que les répertoires racine sont plus proches).</span><span class="sxs-lookup"><span data-stu-id="242b4-220">Make sure the project type is set to **3D**, and set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="242b4-221">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="242b4-221">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab310-22.png)

3.  <span data-ttu-id="242b4-222">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="242b4-222">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="242b4-223">Accédez à **modifier* > les*Préférences\*\* , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="242b4-223">Go to **Edit* > *Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="242b4-224">Remplacez l' **éditeur de script externe** par **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="242b4-224">Change **External Script Editor** to **Visual Studio**.</span></span> <span data-ttu-id="242b4-225">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="242b4-225">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab310-23.png)

4.  <span data-ttu-id="242b4-226">Accédez ensuite à **fichier > paramètres de build** et basculez la **plateforme** sur *plateforme Windows universelle*, puis cliquez sur le bouton **changer de plateforme** .</span><span class="sxs-lookup"><span data-stu-id="242b4-226">Next, go to **File > Build Settings** and switch the **Platform** to *Universal Windows Platform*, and then clicking on the **Switch Platform** button.</span></span>

    ![](images/AzureLabs-Lab310-24.png)

5.  <span data-ttu-id="242b4-227">Dans la même fenêtre **paramètres de build** , vérifiez que les éléments suivants sont définis:</span><span class="sxs-lookup"><span data-stu-id="242b4-227">In the same **Build Settings** window, ensure the following are set:</span></span>

    1.  <span data-ttu-id="242b4-228">L' **appareil cible** est défini sur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="242b4-228">**Target Device** is set to **HoloLens**</span></span>        
    2.  <span data-ttu-id="242b4-229">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="242b4-229">**Build Type** is set to **D3D**</span></span>
    3.  <span data-ttu-id="242b4-230">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="242b4-230">**SDK** is set to **Latest installed**</span></span>
    4.  <span data-ttu-id="242b4-231">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="242b4-231">**Visual Studio Version** is set to **Latest installed**</span></span>
    5.  <span data-ttu-id="242b4-232">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="242b4-232">**Build and Run** is set to **Local Machine**</span></span>            
    6.  <span data-ttu-id="242b4-233">Les paramètres restants, dans **paramètres de build**, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="242b4-233">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

        ![](images/AzureLabs-Lab310-25.png)

6.  <span data-ttu-id="242b4-234">Dans la même fenêtre **paramètres de build** , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' **inspecteur** .</span><span class="sxs-lookup"><span data-stu-id="242b4-234">In the same **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

7. <span data-ttu-id="242b4-235">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="242b4-235">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="242b4-236">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="242b4-236">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="242b4-237">La **version du runtime de script** doit être **expérimentale** (.net 4,6 équivalent), ce qui déclenche la nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="242b4-237">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="242b4-238">Le **serveur principal de script** doit être **.net**.</span><span class="sxs-lookup"><span data-stu-id="242b4-238">**Scripting Backend** should be **.NET**.</span></span>

        3. <span data-ttu-id="242b4-239">Le **niveau de compatibilité** de l’API doit être **.net 4,6**.</span><span class="sxs-lookup"><span data-stu-id="242b4-239">**API Compatibility Level** should be **.NET 4.6**.</span></span>

            ![](images/AzureLabs-Lab310-26.png)

    2.  <span data-ttu-id="242b4-240">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="242b4-240">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="242b4-241">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="242b4-241">**InternetClient**</span></span>

        2.  <span data-ttu-id="242b4-242">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="242b4-242">**Webcam**</span></span>

        3. <span data-ttu-id="242b4-243">**SpatialPerception**</span><span class="sxs-lookup"><span data-stu-id="242b4-243">**SpatialPerception**</span></span>

            <span data-ttu-id="242b4-244">![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)</span><span class="sxs-lookup"><span data-stu-id="242b4-244">![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)</span></span>

    3.  <span data-ttu-id="242b4-245">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, puis assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="242b4-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, then make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![](images/AzureLabs-Lab310-29.png)

8.  <span data-ttu-id="242b4-246">De retour dans les **paramètres de build**, les *projets Unity C\#*  ne sont plus grisés: cochez la case en regard de celle-ci.</span><span class="sxs-lookup"><span data-stu-id="242b4-246">Back in **Build Settings**, *Unity C\# Projects* is no longer greyed out: tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="242b4-247">Fermez la fenêtre **paramètres de build** .</span><span class="sxs-lookup"><span data-stu-id="242b4-247">Close the **Build Settings** window.</span></span>

10. <span data-ttu-id="242b4-248">Dans l' **éditeur**, cliquez sur **modifier** > les**paramètres** > du projet**graphiques**.</span><span class="sxs-lookup"><span data-stu-id="242b4-248">In the **Editor**, click on **Edit** > **Project Settings** > **Graphics**.</span></span>

    ![](images/AzureLabs-Lab310-30.png)

11. <span data-ttu-id="242b4-249">Dans le **panneau Inspecteur** , les *paramètres graphiques* sont ouverts.</span><span class="sxs-lookup"><span data-stu-id="242b4-249">In the **Inspector Panel** the *Graphics Settings* will be open.</span></span> <span data-ttu-id="242b4-250">Faites défiler jusqu’à ce que vous voyez un tableau appelé **toujours inclure**des nuanceurs.</span><span class="sxs-lookup"><span data-stu-id="242b4-250">Scroll down until you see an array called **Always Include Shaders**.</span></span> <span data-ttu-id="242b4-251">Ajoutez un emplacement en accroissant la variable de **taille** d’une unité (dans cet exemple, il s’agissait de 8, nous l’avons rendu 9).</span><span class="sxs-lookup"><span data-stu-id="242b4-251">Add a slot by increasing the **Size** variable by one (in this example, it was 8 so we made it 9).</span></span> <span data-ttu-id="242b4-252">Un nouvel emplacement s’affiche à la dernière position du tableau, comme indiqué ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="242b4-252">A new slot will appear, in the last position of the array, as shown below:</span></span>

    ![](images/AzureLabs-Lab310-31.png)

12. <span data-ttu-id="242b4-253">Dans l’emplacement, cliquez sur le petit cercle cible en regard de l’emplacement pour ouvrir une liste de nuanceurs.</span><span class="sxs-lookup"><span data-stu-id="242b4-253">In the slot, click on the small target circle next to the slot to open a list of shaders.</span></span> <span data-ttu-id="242b4-254">Recherchez les nuanceurs **hérités/transparent/diffus** , puis double-cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="242b4-254">Look for the **Legacy Shaders/Transparent/Diffuse** shader and double-click it.</span></span> 

    ![](images/AzureLabs-Lab310-32.png)

## <a name="chapter-4---importing-the-customvisionobjdetection-unity-package"></a><span data-ttu-id="242b4-255">Chapitre 4-importation du package CustomVisionObjDetection Unity</span><span class="sxs-lookup"><span data-stu-id="242b4-255">Chapter 4 - Importing the CustomVisionObjDetection Unity package</span></span>

<span data-ttu-id="242b4-256">Pour ce cours, vous disposez d’un package d’actifs Unity appelé **Azure-Mr-310. pour Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-256">For this course you are provided with a Unity Asset Package called **Azure-MR-310.unitypackage**.</span></span> 

> <span data-ttu-id="242b4-257">ACCÉLÉRATRICE Tous les objets pris en charge par Unity, y compris les scènes entières, peuvent être empaquetés dans un fichier **. pour Unity** , et exportés/importés dans d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="242b4-257">[TIP] Any objects supported by Unity, including entire scenes, can be packaged into a **.unitypackage** file, and exported / imported in other projects.</span></span> <span data-ttu-id="242b4-258">Il s’agit du moyen le plus sûr et le plus efficace de déplacer des éléments multimédias entre différents **projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-258">It is the safest, and most efficient, way to move assets between different **Unity projects**.</span></span>

<span data-ttu-id="242b4-259">Vous trouverez le [package Azure-Mr-310 que vous devez télécharger ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="242b4-259">You can find the [Azure-MR-310 package that you need to download here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).</span></span>

1.  <span data-ttu-id="242b4-260">Avec le tableau de bord Unity devant vous, cliquez sur **ressources** dans le menu en haut de l’écran, puis sur **importer le package > package personnalisé**.</span><span class="sxs-lookup"><span data-stu-id="242b4-260">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package > Custom Package**.</span></span>

    ![](images/AzureLabs-Lab310-33.png)

2.  <span data-ttu-id="242b4-261">Utilisez le sélecteur de fichiers pour sélectionner le package **Azure-Mr-310. pour Unity** , puis cliquez sur **ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="242b4-261">Use the file picker to select the **Azure-MR-310.unitypackage** package and click **Open**.</span></span> <span data-ttu-id="242b4-262">La liste des composants de cet élément multimédia vous est présentée.</span><span class="sxs-lookup"><span data-stu-id="242b4-262">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="242b4-263">Confirmez l’importation en cliquant sur le bouton **Importer** .</span><span class="sxs-lookup"><span data-stu-id="242b4-263">Confirm the import by clicking the **Import** button.</span></span>

    ![](images/AzureLabs-Lab310-34.png)

3.  <span data-ttu-id="242b4-264">Une fois l’importation terminée, vous remarquerez que les dossiers du package ont été ajoutés à votre dossier de **ressources** .</span><span class="sxs-lookup"><span data-stu-id="242b4-264">Once it has finished importing, you will notice that folders from the package have now been added to your **Assets** folder.</span></span> <span data-ttu-id="242b4-265">Ce type de structure de dossiers est courant pour un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="242b4-265">This kind of folder structure is typical for a Unity project.</span></span>

    ![](images/AzureLabs-Lab310-35.png)

    1.  <span data-ttu-id="242b4-266">Le dossier Materials contient les éléments utilisés par le **curseur en regard**.</span><span class="sxs-lookup"><span data-stu-id="242b4-266">The **Materials** folder contains the material used by the **Gaze Cursor**.</span></span> 

    2.  <span data-ttu-id="242b4-267">Le dossier **plug-ins** contient la dll Newtonsoft utilisée par le code pour désérialiser la réponse Web du service.</span><span class="sxs-lookup"><span data-stu-id="242b4-267">The **Plugins** folder contains the Newtonsoft DLL used by the code to deserialize the Service web response.</span></span> <span data-ttu-id="242b4-268">Les deux (2) différentes versions contenues dans le dossier, et sous-dossier, sont nécessaires pour permettre à la bibliothèque d’être utilisée et construite à la fois par l’éditeur Unity et par la build UWP.</span><span class="sxs-lookup"><span data-stu-id="242b4-268">The two (2) different versions contained in the folder, and sub-folder, are necessary to allow the library to be used and built by both the Unity Editor and the UWP build.</span></span> 

    3.  <span data-ttu-id="242b4-269">Le dossier **Prefabs** contient le Prefabs contenu dans la scène.</span><span class="sxs-lookup"><span data-stu-id="242b4-269">The **Prefabs** folder contains the prefabs contained in the scene.</span></span> <span data-ttu-id="242b4-270">Celles-ci sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-270">Those are:</span></span>

        1.  <span data-ttu-id="242b4-271">**GazeCursor**, le curseur utilisé dans l’application.</span><span class="sxs-lookup"><span data-stu-id="242b4-271">The **GazeCursor**, the cursor used in the application.</span></span> <span data-ttu-id="242b4-272">Fonctionne conjointement avec le Prefab SpatialMapping pour pouvoir être placé dans la scène au-dessus des objets physiques.</span><span class="sxs-lookup"><span data-stu-id="242b4-272">Will work together with the SpatialMapping prefab to be able to be placed in the scene on top of physical objects.</span></span>
        2.  <span data-ttu-id="242b4-273">L' **étiquette**, qui est l’objet d’interface utilisateur utilisé pour afficher la balise d’objet dans la scène, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="242b4-273">The **Label**, which is the UI object used to display the object tag in the scene when required.</span></span>
        3.  <span data-ttu-id="242b4-274">**SpatialMapping**, qui est l’objet qui permet à l’application d’utiliser la création d’une carte virtuelle, à l’aide du suivi spatial Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="242b4-274">The **SpatialMapping**, which is the object that enables the application to use create a virtual map, using the Microsoft HoloLens' spatial tracking.</span></span>

    4.  <span data-ttu-id="242b4-275">Le dossier scenes qui contient actuellement la scène prédéfinie pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="242b4-275">The **Scenes** folder which currently contains the pre-built scene for this course.</span></span>

4.  <span data-ttu-id="242b4-276">Ouvrez le dossier scenes, dans le **panneau Projet**, puis double-cliquez sur **ObjDetectionScene**pour charger la scène que vous allez utiliser pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="242b4-276">Open the **Scenes** folder, in the **Project Panel**, and double-click on the **ObjDetectionScene**, to load the scene that you will use for this course.</span></span>

    ![](images/AzureLabs-Lab310-36.png)

    > [!NOTE] 
    >  <span data-ttu-id="242b4-277">**Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.</span><span class="sxs-lookup"><span data-stu-id="242b4-277">**No code is included**, you will write the code by following this course.</span></span>

## <a name="chapter-5---create-the-customvisionanalyser-class"></a><span data-ttu-id="242b4-278">Chapitre 5-créer la classe CustomVisionAnalyser.</span><span class="sxs-lookup"><span data-stu-id="242b4-278">Chapter 5 - Create the CustomVisionAnalyser class.</span></span>

<span data-ttu-id="242b4-279">À ce stade, vous êtes prêt à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="242b4-279">At this point you are ready to write some code.</span></span> <span data-ttu-id="242b4-280">Vous allez commencer par la classe **CustomVisionAnalyser** .</span><span class="sxs-lookup"><span data-stu-id="242b4-280">You will begin with the **CustomVisionAnalyser** class.</span></span>

> [!NOTE]
> <span data-ttu-id="242b4-281">Les appels à la **service vision personnalisée**, effectués dans le code ci-dessous, sont effectués à l’aide de l' **API REST Custom vision**.</span><span class="sxs-lookup"><span data-stu-id="242b4-281">The calls to the **Custom Vision Service**, made in the code shown below, are made using the **Custom Vision REST API**.</span></span> <span data-ttu-id="242b4-282">À l’aide de ce guide, vous allez apprendre à implémenter et à utiliser cette API (utile pour comprendre comment implémenter des éléments similaires).</span><span class="sxs-lookup"><span data-stu-id="242b4-282">Through using this, you will see how to implement and make use of this API (useful for understanding how to implement something similar on your own).</span></span> <span data-ttu-id="242b4-283">Sachez que Microsoft propose un **Kit de développement logiciel (SDK) Custom vision** qui peut également être utilisé pour effectuer des appels au service.</span><span class="sxs-lookup"><span data-stu-id="242b4-283">Be aware, that Microsoft offers a **Custom Vision SDK** that can also be used to make calls to the Service.</span></span> <span data-ttu-id="242b4-284">Pour plus d’informations, consultez l' [article du kit de développement logiciel (SDK) Custom vision](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).</span><span class="sxs-lookup"><span data-stu-id="242b4-284">For more information visit the [Custom Vision SDK article](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).</span></span>

<span data-ttu-id="242b4-285">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-285">This class is responsible for:</span></span>

- <span data-ttu-id="242b4-286">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="242b4-286">Loading the latest image captured as an array of bytes.</span></span>

- <span data-ttu-id="242b4-287">Envoi du tableau d’octets à votre instance Azure **service vision personnalisée** à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="242b4-287">Sending the byte array to your Azure **Custom Vision Service** instance for analysis.</span></span>

- <span data-ttu-id="242b4-288">Réception de la réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="242b4-288">Receiving the response as a JSON string.</span></span>

- <span data-ttu-id="242b4-289">La désérialisation de la réponse et le passage de la prédiction résultante à la classe **SceneOrganiser** , qui s’occupera du mode d’affichage de la réponse.</span><span class="sxs-lookup"><span data-stu-id="242b4-289">Deserializing the response and passing the resulting **Prediction** to the **SceneOrganiser** class, which will take care of how the response should be displayed.</span></span>

<span data-ttu-id="242b4-290">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-290">To create this class:</span></span>

1.  <span data-ttu-id="242b4-291">Cliquez avec le bouton droit sur le **dossier Asset**, situé dans le **panneau Projet**, puis cliquez sur **créer** > un**dossier**.</span><span class="sxs-lookup"><span data-stu-id="242b4-291">Right-click in the **Asset Folder**, located in the **Project Panel**, then click **Create** > **Folder**.</span></span> <span data-ttu-id="242b4-292">Appelez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="242b4-292">Call the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab310-37.png)

2.  <span data-ttu-id="242b4-293">Double-cliquez sur le dossier nouvellement créé pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="242b4-293">Double-click on the newly created folder, to open it.</span></span>

3.  <span data-ttu-id="242b4-294">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-294">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-295">Nommez le script **CustomVisionAnalyser.**</span><span class="sxs-lookup"><span data-stu-id="242b4-295">Name the script **CustomVisionAnalyser.**</span></span>

4.  <span data-ttu-id="242b4-296">Double-cliquez sur le nouveau script **CustomVisionAnalyser** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-296">Double-click on the new **CustomVisionAnalyser** script to open it with **Visual Studio.**</span></span>

5.  <span data-ttu-id="242b4-297">Assurez-vous que les espaces de noms suivants sont référencés en haut du fichier:</span><span class="sxs-lookup"><span data-stu-id="242b4-297">Make sure you have the following namespaces referenced at the top of the file:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

6.  <span data-ttu-id="242b4-298">Dans la classe **CustomVisionAnalyser** , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-298">In the **CustomVisionAnalyser** class, add the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Unique instance of this class
        /// </summary>
        public static CustomVisionAnalyser Instance;

        /// <summary>
        /// Insert your prediction key here
        /// </summary>
        private string predictionKey = "- Insert your key here -";

        /// <summary>
        /// Insert your prediction endpoint here
        /// </summary>
        private string predictionEndpoint = "Insert your prediction endpoint here";

        /// <summary>
        /// Bite array of the image to submit for analysis
        /// </summary>
        [HideInInspector] public byte[] imageBytes;
    ```

    > [!NOTE]
    > <span data-ttu-id="242b4-299">Veillez à insérer votre **clé de prédiction de service** dans la variable **PredictionKey** et votre **point de terminaison de prédiction** dans la variable **predictionEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="242b4-299">Make sure you insert your **Service Prediction-Key** into the **predictionKey** variable and your **Prediction-Endpoint** into the **predictionEndpoint** variable.</span></span> <span data-ttu-id="242b4-300">Vous les avez copiées [précédemment dans le bloc-notes, au chapitre 2, étape 14](#chapter-2---training-your-custom-vision-project).</span><span class="sxs-lookup"><span data-stu-id="242b4-300">You copied these to [Notepad earlier, in Chapter 2, Step 14](#chapter-2---training-your-custom-vision-project).</span></span>

7.  <span data-ttu-id="242b4-301">Le code pour **éveillé ()** doit maintenant être ajouté pour initialiser la variable d’instance:</span><span class="sxs-lookup"><span data-stu-id="242b4-301">Code for **Awake()** now needs to be added to initialize the Instance variable:</span></span>

    ```csharp
        /// <summary>
        /// Initializes this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }
    ```

8.  <span data-ttu-id="242b4-302">Ajoutez la Coroutine (avec la méthode statique **GetImageAsByteArray ()** en dessous de celle-ci), qui obtiendra les résultats de l’analyse de l’image, capturés par la classe **ImageCapture** .</span><span class="sxs-lookup"><span data-stu-id="242b4-302">Add the coroutine (with the static **GetImageAsByteArray()** method below it), which will obtain the results of the analysis of the image, captured by the **ImageCapture** class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="242b4-303">Dans la Coroutine **AnalyseImageCapture** , il y a un appel à la classe **SceneOrganiser** que vous êtes encore en cours de création.</span><span class="sxs-lookup"><span data-stu-id="242b4-303">In the **AnalyseImageCapture** coroutine, there is a call to the **SceneOrganiser** class that you are yet to create.</span></span> <span data-ttu-id="242b4-304">Par conséquent, **laissez ces lignes commentées pour l’instant**.</span><span class="sxs-lookup"><span data-stu-id="242b4-304">Therefore, **leave those lines commented for now**.</span></span>

    ```csharp    
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured(string imagePath)
        {
            Debug.Log("Analyzing...");

            WWWForm webForm = new WWWForm();

            using (UnityWebRequest unityWebRequest = UnityWebRequest.Post(predictionEndpoint, webForm))
            {
                // Gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);

                unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                unityWebRequest.SetRequestHeader("Prediction-Key", predictionKey);

                // The upload handler will help uploading the byte array with the request
                unityWebRequest.uploadHandler = new UploadHandlerRaw(imageBytes);
                unityWebRequest.uploadHandler.contentType = "application/octet-stream";

                // The download handler will help receiving the analysis from Azure
                unityWebRequest.downloadHandler = new DownloadHandlerBuffer();

                // Send the request
                yield return unityWebRequest.SendWebRequest();

                string jsonResponse = unityWebRequest.downloadHandler.text;

                Debug.Log("response: " + jsonResponse);

                // Create a texture. Texture size does not matter, since
                // LoadImage will replace with the incoming image size.
                //Texture2D tex = new Texture2D(1, 1);
                //tex.LoadImage(imageBytes);
                //SceneOrganiser.Instance.quadRenderer.material.SetTexture("_MainTex", tex);

                // The response will be in JSON format, therefore it needs to be deserialized
                //AnalysisRootObject analysisRootObject = new AnalysisRootObject();
                //analysisRootObject = JsonConvert.DeserializeObject<AnalysisRootObject>(jsonResponse);

                //SceneOrganiser.Instance.FinaliseLabel(analysisRootObject);
            }
        }

        /// <summary>
        /// Returns the contents of the specified image file as a byte array.
        /// </summary>
        static byte[] GetImageAsByteArray(string imageFilePath)
        {
            FileStream fileStream = new FileStream(imageFilePath, FileMode.Open, FileAccess.Read);

            BinaryReader binaryReader = new BinaryReader(fileStream);

            return binaryReader.ReadBytes((int)fileStream.Length);
        }
    ```

9. <span data-ttu-id="242b4-305">Supprimez les méthodes **Start ()** et **Update ()** , car elles ne seront pas utilisées.</span><span class="sxs-lookup"><span data-stu-id="242b4-305">Delete the **Start()** and **Update()** methods, as they will not be used.</span></span> 

10.  <span data-ttu-id="242b4-306">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-306">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="242b4-307">Comme mentionné précédemment, ne vous inquiétez pas du code qui peut sembler avoir une erreur, car vous fournirez bientôt d’autres classes, ce qui les corrigera.</span><span class="sxs-lookup"><span data-stu-id="242b4-307">As mentioned earlier, do not worry about code which might appear to have an error, as you will provide further classes soon, which will fix these.</span></span>

## <a name="chapter-6---create-the-customvisionobjects-class"></a><span data-ttu-id="242b4-308">Chapitre 6-créer la classe CustomVisionObjects</span><span class="sxs-lookup"><span data-stu-id="242b4-308">Chapter 6 - Create the CustomVisionObjects class</span></span>

<span data-ttu-id="242b4-309">La classe que vous allez créer est maintenant la classe **CustomVisionObjects** .</span><span class="sxs-lookup"><span data-stu-id="242b4-309">The class you will create now is the **CustomVisionObjects** class.</span></span>

<span data-ttu-id="242b4-310">Ce script contient un certain nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels passés au Service Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="242b4-310">This script contains a number of objects used by other classes to serialize and deserialize the calls made to the Custom Vision Service.</span></span>

<span data-ttu-id="242b4-311">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-311">To create this class:</span></span>

1.  <span data-ttu-id="242b4-312">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-312">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-313">Appelez le script **CustomVisionObjects.**</span><span class="sxs-lookup"><span data-stu-id="242b4-313">Call the script **CustomVisionObjects.**</span></span>

2.  <span data-ttu-id="242b4-314">Double-cliquez sur le nouveau script **CustomVisionObjects** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-314">Double-click on the new **CustomVisionObjects** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="242b4-315">Assurez-vous que les espaces de noms suivants sont référencés en haut du fichier:</span><span class="sxs-lookup"><span data-stu-id="242b4-315">Make sure you have the following namespaces referenced at the top of the file:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="242b4-316">Supprimez les méthodes **Start ()** et **Update ()** à l’intérieur de la classe **CustomVisionObjects** , cette classe doit maintenant être vide.</span><span class="sxs-lookup"><span data-stu-id="242b4-316">Delete the **Start()** and **Update()** methods inside the **CustomVisionObjects** class, this class should now be empty.</span></span>

    > [!WARNING]
    > <span data-ttu-id="242b4-317">Il est important de suivre attentivement l’instruction suivante.</span><span class="sxs-lookup"><span data-stu-id="242b4-317">It is important you follow the next instruction carefully.</span></span> <span data-ttu-id="242b4-318">Si vous placez les nouvelles déclarations de classe à l’intérieur de la classe **CustomVisionObjects** , vous obtiendrez des erreurs de compilation dans le [chapitre 10](#chapter-10---create-the-imagecapture-class), indiquant que **AnalysisRootObject** et **BoundingBox** sont introuvables.</span><span class="sxs-lookup"><span data-stu-id="242b4-318">If you put the new class declarations inside the **CustomVisionObjects** class, you will get compile errors in [chapter 10](#chapter-10---create-the-imagecapture-class), stating that **AnalysisRootObject** and **BoundingBox** are not found.</span></span>

5.  <span data-ttu-id="242b4-319">Ajoutez les classes suivantes *en dehors* de la classe **CustomVisionObjects** .</span><span class="sxs-lookup"><span data-stu-id="242b4-319">Add the following classes *outside* the **CustomVisionObjects** class.</span></span> <span data-ttu-id="242b4-320">Ces objets sont utilisés par la bibliothèque **Newtonsoft** pour sérialiser et désérialiser les données de réponse:</span><span class="sxs-lookup"><span data-stu-id="242b4-320">These objects are used by the **Newtonsoft** library to serialize and deserialize the response data:</span></span>

    ```csharp
    // The objects contained in this script represent the deserialized version
    // of the objects used by this application 

    /// <summary>
    /// Web request object for image data
    /// </summary>
    class MultipartObject : IMultipartFormSection
    {
        public string sectionName { get; set; }

        public byte[] sectionData { get; set; }

        public string fileName { get; set; }

        public string contentType { get; set; }
    }

    /// <summary>
    /// JSON of all Tags existing within the project
    /// contains the list of Tags
    /// </summary> 
    public class Tags_RootObject
    {
        public List<TagOfProject> Tags { get; set; }
        public int TotalTaggedImages { get; set; }
        public int TotalUntaggedImages { get; set; }
    }

    public class TagOfProject
    {
        public string Id { get; set; }
        public string Name { get; set; }
        public string Description { get; set; }
        public int ImageCount { get; set; }
    }

    /// <summary>
    /// JSON of Tag to associate to an image
    /// Contains a list of hosting the tags,
    /// since multiple tags can be associated with one image
    /// </summary> 
    public class Tag_RootObject
    {
        public List<Tag> Tags { get; set; }
    }

    public class Tag
    {
        public string ImageId { get; set; }
        public string TagId { get; set; }
    }

    /// <summary>
    /// JSON of images submitted
    /// Contains objects that host detailed information about one or more images
    /// </summary> 
    public class ImageRootObject
    {
        public bool IsBatchSuccessful { get; set; }
        public List<SubmittedImage> Images { get; set; }
    }

    public class SubmittedImage
    {
        public string SourceUrl { get; set; }
        public string Status { get; set; }
        public ImageObject Image { get; set; }
    }

    public class ImageObject
    {
        public string Id { get; set; }
        public DateTime Created { get; set; }
        public int Width { get; set; }
        public int Height { get; set; }
        public string ImageUri { get; set; }
        public string ThumbnailUri { get; set; }
    }

    /// <summary>
    /// JSON of Service Iteration
    /// </summary> 
    public class Iteration
    {
        public string Id { get; set; }
        public string Name { get; set; }
        public bool IsDefault { get; set; }
        public string Status { get; set; }
        public string Created { get; set; }
        public string LastModified { get; set; }
        public string TrainedAt { get; set; }
        public string ProjectId { get; set; }
        public bool Exportable { get; set; }
        public string DomainId { get; set; }
    }

    /// <summary>
    /// Predictions received by the Service
    /// after submitting an image for analysis
    /// Includes Bounding Box
    /// </summary>
    public class AnalysisRootObject
    {
        public string id { get; set; }
        public string project { get; set; }
        public string iteration { get; set; }
        public DateTime created { get; set; }
        public List<Prediction> predictions { get; set; }
    }

    public class BoundingBox
    {
        public double left { get; set; }
        public double top { get; set; }
        public double width { get; set; }
        public double height { get; set; }
    }

    public class Prediction
    {
        public double probability { get; set; }
        public string tagId { get; set; }
        public string tagName { get; set; }
        public BoundingBox boundingBox { get; set; }
    }
    ```

6.  <span data-ttu-id="242b4-321">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-321">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-7---create-the-spatialmapping-class"></a><span data-ttu-id="242b4-322">Chapitre 7-créer la classe SpatialMapping</span><span class="sxs-lookup"><span data-stu-id="242b4-322">Chapter 7 - Create the SpatialMapping class</span></span>

<span data-ttu-id="242b4-323">Cette classe définit le **conflit de mappage spatial** dans la scène afin de pouvoir détecter les collisions entre les objets virtuels et les objets réels.</span><span class="sxs-lookup"><span data-stu-id="242b4-323">This class will set the **Spatial Mapping Collider** in the scene so to be able to detect collisions between virtual objects and real objects.</span></span>

<span data-ttu-id="242b4-324">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-324">To create this class:</span></span>

1.  <span data-ttu-id="242b4-325">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-325">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-326">Appelez le script **SpatialMapping.**</span><span class="sxs-lookup"><span data-stu-id="242b4-326">Call the script **SpatialMapping.**</span></span>

2.  <span data-ttu-id="242b4-327">Double-cliquez sur le nouveau script **SpatialMapping** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-327">Double-click on the new **SpatialMapping** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="242b4-328">Assurez-vous que les espaces de noms suivants sont référencés au-dessus de la classe **SpatialMapping** :</span><span class="sxs-lookup"><span data-stu-id="242b4-328">Make sure you have the following namespaces referenced above the **SpatialMapping** class:</span></span>

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA;
    ```

4.  <span data-ttu-id="242b4-329">Ensuite, ajoutez les variables suivantes à l’intérieur de la classe **SpatialMapping** , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="242b4-329">Then, add the following variables inside the **SpatialMapping** class, above the **Start()** method:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SpatialMapping Instance;

        /// <summary>
        /// Used by the GazeCursor as a property with the Raycast call
        /// </summary>
        internal static int PhysicsRaycastMask;

        /// <summary>
        /// The layer to use for spatial mapping collisions
        /// </summary>
        internal int physicsLayer = 31;

        /// <summary>
        /// Creates environment colliders to work with physics
        /// </summary>
        private SpatialMappingCollider spatialMappingCollider;
    ```

5.  <span data-ttu-id="242b4-330">Ajoutez les éléments **éveillé ()** et **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="242b4-330">Add the **Awake()** and **Start()**:</span></span>

    ```csharp
        /// <summary>
        /// Initializes this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }

        /// <summary>
        /// Runs at initialization right after Awake method
        /// </summary>
        void Start()
        {
            // Initialize and configure the collider
            spatialMappingCollider = gameObject.GetComponent<SpatialMappingCollider>();
            spatialMappingCollider.surfaceParent = this.gameObject;
            spatialMappingCollider.freezeUpdates = false;
            spatialMappingCollider.layer = physicsLayer;

            // define the mask
            PhysicsRaycastMask = 1 << physicsLayer;

            // set the object as active one
            gameObject.SetActive(true);
        }
    ```

6.  <span data-ttu-id="242b4-331">Supprimez la méthode **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="242b4-331">Delete the **Update()** method.</span></span>

7.  <span data-ttu-id="242b4-332">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-332">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>


## <a name="chapter-8---create-the-gazecursor-class"></a><span data-ttu-id="242b4-333">Chapitre 8-créer la classe GazeCursor</span><span class="sxs-lookup"><span data-stu-id="242b4-333">Chapter 8 - Create the GazeCursor class</span></span>

<span data-ttu-id="242b4-334">Cette classe est chargée de configurer le curseur à l’emplacement approprié dans l’espace réel, en utilisant le **SpatialMappingCollider**créé dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="242b4-334">This class is responsible for setting up the cursor in the correct location in real space, by making use of the **SpatialMappingCollider**, created in the previous chapter.</span></span>

<span data-ttu-id="242b4-335">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-335">To create this class:</span></span>

1.  <span data-ttu-id="242b4-336">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-336">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-337">Appeler le script **GazeCursor**</span><span class="sxs-lookup"><span data-stu-id="242b4-337">Call the script **GazeCursor**</span></span>

2.  <span data-ttu-id="242b4-338">Double-cliquez sur le nouveau script **GazeCursor** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-338">Double-click on the new **GazeCursor** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="242b4-339">Assurez-vous que l’espace de noms suivant est référencé au-dessus de la classe **GazeCursor** :</span><span class="sxs-lookup"><span data-stu-id="242b4-339">Make sure you have the following namespace referenced above the **GazeCursor** class:</span></span>

    ```csharp
    using UnityEngine;
    ```

4.  <span data-ttu-id="242b4-340">Ajoutez ensuite la variable suivante à l’intérieur de la classe **GazeCursor** , au-dessus de la méthode **Start ()** .</span><span class="sxs-lookup"><span data-stu-id="242b4-340">Then add the following variable inside the **GazeCursor** class, above the **Start()** method.</span></span> 

    ```csharp
        /// <summary>
        /// The cursor (this object) mesh renderer
        /// </summary>
        private MeshRenderer meshRenderer;
    ```

5.  <span data-ttu-id="242b4-341">Mettez à jour la méthode **Start ()** avec le code suivant:</span><span class="sxs-lookup"><span data-stu-id="242b4-341">Update the **Start()** method with the following code:</span></span>

    ```csharp
        /// <summary>
        /// Runs at initialization right after the Awake method
        /// </summary>
        void Start()
        {
            // Grab the mesh renderer that is on the same object as this script.
            meshRenderer = gameObject.GetComponent<MeshRenderer>();

            // Set the cursor reference
            SceneOrganiser.Instance.cursor = gameObject;
            gameObject.GetComponent<Renderer>().material.color = Color.green;

            // If you wish to change the size of the cursor you can do so here
            gameObject.transform.localScale = new Vector3(0.01f, 0.01f, 0.01f);
        }
    ```

6.  <span data-ttu-id="242b4-342">Mettez à jour la méthode **Update ()** avec le code suivant:</span><span class="sxs-lookup"><span data-stu-id="242b4-342">Update the **Update()** method with the following code:</span></span>

    ```csharp
        /// <summary>
        /// Update is called once per frame
        /// </summary>
        void Update()
        {
            // Do a raycast into the world based on the user's head position and orientation.
            Vector3 headPosition = Camera.main.transform.position;
            Vector3 gazeDirection = Camera.main.transform.forward;

            RaycastHit gazeHitInfo;
            if (Physics.Raycast(headPosition, gazeDirection, out gazeHitInfo, 30.0f, SpatialMapping.PhysicsRaycastMask))
            {
                // If the raycast hit a hologram, display the cursor mesh.
                meshRenderer.enabled = true;
                // Move the cursor to the point where the raycast hit.
                transform.position = gazeHitInfo.point;
                // Rotate the cursor to hug the surface of the hologram.
                transform.rotation = Quaternion.FromToRotation(Vector3.up, gazeHitInfo.normal);
            }
            else
            {
                // If the raycast did not hit a hologram, hide the cursor mesh.
                meshRenderer.enabled = false;
            }
        }
    ```

    > [!NOTE]
    > <span data-ttu-id="242b4-343">Ne vous inquiétez pas de l’erreur pour la classe **SceneOrganiser** introuvable, vous allez la créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="242b4-343">Do not worry about the error for the **SceneOrganiser** class not being found, you will create it in the next chapter.</span></span>

7. <span data-ttu-id="242b4-344">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-344">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-9---create-the-sceneorganiser-class"></a><span data-ttu-id="242b4-345">Chapitre 9-créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="242b4-345">Chapter 9 - Create the SceneOrganiser class</span></span>

<span data-ttu-id="242b4-346">Cette classe effectuera les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-346">This class will:</span></span>

-   <span data-ttu-id="242b4-347">Configurez la *caméra principale* en y joignant les composants appropriés.</span><span class="sxs-lookup"><span data-stu-id="242b4-347">Set up the *Main Camera* by attaching the appropriate components to it.</span></span>

-   <span data-ttu-id="242b4-348">Lorsqu’un objet est détecté, il est chargé de calculer sa position dans le monde réel et de placer une **étiquette** de balise près de celui-ci avec le **nom**de balise approprié.</span><span class="sxs-lookup"><span data-stu-id="242b4-348">When an object is detected, it will be responsible for calculating its position in the real world and place a **Tag Label** near it with the appropriate **Tag Name**.</span></span>    

<span data-ttu-id="242b4-349">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-349">To create this class:</span></span>

1.  <span data-ttu-id="242b4-350">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-350">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-351">Nommez le script **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="242b4-351">Name the script **SceneOrganiser**.</span></span>

2.  <span data-ttu-id="242b4-352">Double-cliquez sur le nouveau script **SceneOrganiser** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-352">Double-click on the new **SceneOrganiser** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="242b4-353">Assurez-vous que les espaces de noms suivants sont référencés au-dessus de la classe **SceneOrganiser** :</span><span class="sxs-lookup"><span data-stu-id="242b4-353">Make sure you have the following namespaces referenced above the **SceneOrganiser** class:</span></span>

    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    ```

4.  <span data-ttu-id="242b4-354">Ajoutez ensuite les variables suivantes à l’intérieur de la classe **SceneOrganiser** , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="242b4-354">Then add the following variables inside the **SceneOrganiser** class, above the **Start()** method:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SceneOrganiser Instance;

        /// <summary>
        /// The cursor object attached to the Main Camera
        /// </summary>
        internal GameObject cursor;

        /// <summary>
        /// The label used to display the analysis on the objects in the real world
        /// </summary>
        public GameObject label;

        /// <summary>
        /// Reference to the last Label positioned
        /// </summary>
        internal Transform lastLabelPlaced;

        /// <summary>
        /// Reference to the last Label positioned
        /// </summary>
        internal TextMesh lastLabelPlacedText;

        /// <summary>
        /// Current threshold accepted for displaying the label
        /// Reduce this value to display the recognition more often
        /// </summary>
        internal float probabilityThreshold = 0.8f;

        /// <summary>
        /// The quad object hosting the imposed image captured
        /// </summary>
        private GameObject quad;

        /// <summary>
        /// Renderer of the quad object
        /// </summary>
        internal Renderer quadRenderer;
    ```

5.  <span data-ttu-id="242b4-355">Supprimez les méthodes **Start ()** et **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="242b4-355">Delete the **Start()** and **Update()** methods.</span></span>

6.  <span data-ttu-id="242b4-356">Sous les variables, ajoutez la méthode **éveillé ()** , qui initialisera la classe et configurera la scène.</span><span class="sxs-lookup"><span data-stu-id="242b4-356">Underneath the variables, add the **Awake()** method, which will initialize the class and set up the scene.</span></span>

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            // Use this class instance as singleton
            Instance = this;

            // Add the ImageCapture class to this Gameobject
            gameObject.AddComponent<ImageCapture>();

            // Add the CustomVisionAnalyser class to this Gameobject
            gameObject.AddComponent<CustomVisionAnalyser>();

            // Add the CustomVisionObjects class to this Gameobject
            gameObject.AddComponent<CustomVisionObjects>();
        }
    ```

7.  <span data-ttu-id="242b4-357">Ajoutez la méthode **PlaceAnalysisLabel ()** , qui *instanciera* l’étiquette dans la scène (qui, à ce stade, est invisible pour l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="242b4-357">Add the **PlaceAnalysisLabel()** method, which will *Instantiate* the label in the scene (which at this point is invisible to the user).</span></span> <span data-ttu-id="242b4-358">Il place également le quadruple (également invisible) où l’image est placée et chevauche le monde réel.</span><span class="sxs-lookup"><span data-stu-id="242b4-358">It also places the quad (also invisible) where the image is placed, and overlaps with the real world.</span></span> <span data-ttu-id="242b4-359">Cela est important, car les coordonnées de la zone récupérées à partir du service après l’analyse sont retracées dans ce Quad pour déterminer l’emplacement approximatif de l’objet dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="242b4-359">This is important because the box coordinates retrieved from the Service after analysis are traced back into this quad to determined the approximate location of the object in the real world.</span></span> 

    ```csharp
        /// <summary>
        /// Instantiate a Label in the appropriate location relative to the Main Camera.
        /// </summary>
        public void PlaceAnalysisLabel()
        {
            lastLabelPlaced = Instantiate(label.transform, cursor.transform.position, transform.rotation);
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
            lastLabelPlacedText.text = "";
            lastLabelPlaced.transform.localScale = new Vector3(0.005f,0.005f,0.005f);

            // Create a GameObject to which the texture can be applied
            quad = GameObject.CreatePrimitive(PrimitiveType.Quad);
            quadRenderer = quad.GetComponent<Renderer>() as Renderer;
            Material m = new Material(Shader.Find("Legacy Shaders/Transparent/Diffuse"));
            quadRenderer.material = m;

            // Here you can set the transparency of the quad. Useful for debugging
            float transparency = 0f;
            quadRenderer.material.color = new Color(1, 1, 1, transparency);

            // Set the position and scale of the quad depending on user position
            quad.transform.parent = transform;
            quad.transform.rotation = transform.rotation;

            // The quad is positioned slightly forward in font of the user
            quad.transform.localPosition = new Vector3(0.0f, 0.0f, 3.0f);

            // The quad scale as been set with the following value following experimentation,  
            // to allow the image on the quad to be as precisely imposed to the real world as possible
            quad.transform.localScale = new Vector3(3f, 1.65f, 1f);
            quad.transform.parent = null;
        }
    ```

8.  <span data-ttu-id="242b4-360">Ajoutez la méthode **FinaliseLabel ()** .</span><span class="sxs-lookup"><span data-stu-id="242b4-360">Add the **FinaliseLabel()** method.</span></span> <span data-ttu-id="242b4-361">Il est responsable des tâches suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-361">It is responsible for:</span></span>

    *   <span data-ttu-id="242b4-362">Définition du texte de l' *étiquette* avec la *balise* de la prédiction avec la confiance la plus élevée.</span><span class="sxs-lookup"><span data-stu-id="242b4-362">Setting the *Label* text with the *Tag* of the Prediction with the highest confidence.</span></span>
    *   <span data-ttu-id="242b4-363">Appel du calcul du *cadre englobant* sur l’objet quadruple, positionné précédemment, et placement de l’étiquette dans la scène.</span><span class="sxs-lookup"><span data-stu-id="242b4-363">Calling the calculation of the *Bounding Box* on the quad object, positioned previously, and placing the label in the scene.</span></span>
    *   <span data-ttu-id="242b4-364">Ajustement de la profondeur des étiquettes à l’aide d’un Raycast vers le *cadre englobant*, qui doit entrer en conflit avec l’objet dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="242b4-364">Adjusting the label depth by using a Raycast towards the *Bounding Box*, which should collide against the object in the real world.</span></span>
    * <span data-ttu-id="242b4-365">Réinitialisation du processus de capture pour permettre à l’utilisateur de capturer une autre image.</span><span class="sxs-lookup"><span data-stu-id="242b4-365">Resetting the capture process to allow the user to capture another image.</span></span>

    ```csharp
        /// <summary>
        /// Set the Tags as Text of the last label created. 
        /// </summary>
        public void FinaliseLabel(AnalysisRootObject analysisObject)
        {
            if (analysisObject.predictions != null)
            {
                lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
                // Sort the predictions to locate the highest one
                List<Prediction> sortedPredictions = new List<Prediction>();
                sortedPredictions = analysisObject.predictions.OrderBy(p => p.probability).ToList();
                Prediction bestPrediction = new Prediction();
                bestPrediction = sortedPredictions[sortedPredictions.Count - 1];

                if (bestPrediction.probability > probabilityThreshold)
                {
                    quadRenderer = quad.GetComponent<Renderer>() as Renderer;
                    Bounds quadBounds = quadRenderer.bounds;

                    // Position the label as close as possible to the Bounding Box of the prediction 
                    // At this point it will not consider depth
                    lastLabelPlaced.transform.parent = quad.transform;
                    lastLabelPlaced.transform.localPosition = CalculateBoundingBoxPosition(quadBounds, bestPrediction.boundingBox);

                    // Set the tag text
                    lastLabelPlacedText.text = bestPrediction.tagName;

                    // Cast a ray from the user's head to the currently placed label, it should hit the object detected by the Service.
                    // At that point it will reposition the label where the ray HL sensor collides with the object,
                    // (using the HL spatial tracking)
                    Debug.Log("Repositioning Label");
                    Vector3 headPosition = Camera.main.transform.position;
                    RaycastHit objHitInfo;
                    Vector3 objDirection = lastLabelPlaced.position;
                    if (Physics.Raycast(headPosition, objDirection, out objHitInfo, 30.0f,   SpatialMapping.PhysicsRaycastMask))
                    {
                        lastLabelPlaced.position = objHitInfo.point;
                    }
                }
            }
            // Reset the color of the cursor
            cursor.GetComponent<Renderer>().material.color = Color.green;

            // Stop the analysis process
            ImageCapture.Instance.ResetImageCapture();        
        }
    ```

9.  <span data-ttu-id="242b4-366">Ajoutez la méthode **CalculateBoundingBoxPosition ()** , qui héberge un certain nombre de calculs nécessaires pour convertir les coordonnées du *cadre englobant* récupérées à partir du service et les recréer proportionnellement sur le quadruple.</span><span class="sxs-lookup"><span data-stu-id="242b4-366">Add the **CalculateBoundingBoxPosition()** method, which hosts a number of calculations necessary to translate the *Bounding Box* coordinates retrieved from the Service and recreate them proportionally on the quad.</span></span>

    ```csharp
        /// <summary>
        /// This method hosts a series of calculations to determine the position 
        /// of the Bounding Box on the quad created in the real world
        /// by using the Bounding Box received back alongside the Best Prediction
        /// </summary>
        public Vector3 CalculateBoundingBoxPosition(Bounds b, BoundingBox boundingBox)
        {
            Debug.Log($"BB: left {boundingBox.left}, top {boundingBox.top}, width {boundingBox.width}, height {boundingBox.height}");

            double centerFromLeft = boundingBox.left + (boundingBox.width / 2);
            double centerFromTop = boundingBox.top + (boundingBox.height / 2);
            Debug.Log($"BB CenterFromLeft {centerFromLeft}, CenterFromTop {centerFromTop}");

            double quadWidth = b.size.normalized.x;
            double quadHeight = b.size.normalized.y;
            Debug.Log($"Quad Width {b.size.normalized.x}, Quad Height {b.size.normalized.y}");

            double normalisedPos_X = (quadWidth * centerFromLeft) - (quadWidth/2);
            double normalisedPos_Y = (quadHeight * centerFromTop) - (quadHeight/2);

            return new Vector3((float)normalisedPos_X, (float)normalisedPos_Y, 0);
        }
    ```

10. <span data-ttu-id="242b4-367">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-367">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="242b4-368">Avant de continuer, ouvrez la classe **CustomVisionAnalyser** et, dans la méthode **AnalyseLastImageCaptured ()** , *supprimez les marques de commentaire* des lignes suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-368">Before you continue, open the **CustomVisionAnalyser** class, and within the **AnalyseLastImageCaptured()** method, *uncomment* the following lines:</span></span>
    >
    >   ```csharp
    >   // Create a texture. Texture size does not matter, since 
    >   // LoadImage will replace with the incoming image size.
    >   Texture2D tex = new Texture2D(1, 1);
    >   tex.LoadImage(imageBytes);
    >   SceneOrganiser.Instance.quadRenderer.material.SetTexture("_MainTex", tex);
    >
    >   // The response will be in JSON format, therefore it needs to be deserialized
    >   AnalysisRootObject analysisRootObject = new AnalysisRootObject();
    >   analysisRootObject = JsonConvert.DeserializeObject<AnalysisRootObject>(jsonResponse);
    >
    >   SceneOrganiser.Instance.FinaliseLabel(analysisRootObject);
    >   ```

> [!NOTE]
> <span data-ttu-id="242b4-369">Ne vous inquiétez pas du message «Impossible de trouver la classe **ImageCapture** », vous allez le créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="242b4-369">Do not worry about the **ImageCapture** class 'could not be found' message, you will create it in the next chapter.</span></span>


## <a name="chapter-10---create-the-imagecapture-class"></a><span data-ttu-id="242b4-370">Chapitre 10-créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="242b4-370">Chapter 10 - Create the ImageCapture class</span></span>

<span data-ttu-id="242b4-371">La classe suivante que vous allez créer est la classe **ImageCapture** .</span><span class="sxs-lookup"><span data-stu-id="242b4-371">The next class you are going to create is the **ImageCapture** class.</span></span>

<span data-ttu-id="242b4-372">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="242b4-372">This class is responsible for:</span></span>

*   <span data-ttu-id="242b4-373">Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l' *application* .</span><span class="sxs-lookup"><span data-stu-id="242b4-373">Capturing an image using the HoloLens camera and storing it in the *App* folder.</span></span>
*   <span data-ttu-id="242b4-374">Gestion des gestes *Tap* de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="242b4-374">Handling *Tap* gestures from the user.</span></span>

<span data-ttu-id="242b4-375">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="242b4-375">To create this class:</span></span>

1.  <span data-ttu-id="242b4-376">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="242b4-376">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="242b4-377">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-377">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="242b4-378">Nommez le script **ImageCapture**.</span><span class="sxs-lookup"><span data-stu-id="242b4-378">Name the script **ImageCapture**.</span></span>

3.  <span data-ttu-id="242b4-379">Double-cliquez sur le nouveau script **ImageCapture** pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="242b4-379">Double-click on the new **ImageCapture** script to open it with **Visual Studio.**</span></span>

4.  <span data-ttu-id="242b4-380">Remplacez les espaces de noms en haut du fichier par les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="242b4-380">Replace the namespaces at the top of the file with the following:</span></span>

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="242b4-381">Ajoutez ensuite les variables suivantes à l’intérieur de la classe **ImageCapture** , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="242b4-381">Then add the following variables inside the **ImageCapture** class, above the **Start()** method:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static ImageCapture Instance;

        /// <summary>
        /// Keep counts of the taps for image renaming
        /// </summary>
        private int captureCount = 0;

        /// <summary>
        /// Photo Capture object
        /// </summary>
        private PhotoCapture photoCaptureObject = null;

        /// <summary>
        /// Allows gestures recognition in HoloLens
        /// </summary>
        private GestureRecognizer recognizer;

        /// <summary>
        /// Flagging if the capture loop is running
        /// </summary>
        internal bool captureIsActive;
        
        /// <summary>
        /// File path of current analysed photo
        /// </summary>
        internal string filePath = string.Empty;
    ```

6.  <span data-ttu-id="242b4-382">Vous devez maintenant ajouter le code des méthodes **éveillés ()** et **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="242b4-382">Code for **Awake()** and **Start()** methods now needs to be added:</span></span>

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            Instance = this;
        }

        /// <summary>
        /// Runs at initialization right after Awake method
        /// </summary>
        void Start()
        {
            // Clean up the LocalState folder of this application from all photos stored
            DirectoryInfo info = new DirectoryInfo(Application.persistentDataPath);
            var fileInfo = info.GetFiles();
            foreach (var file in fileInfo)
            {
                try
                {
                    file.Delete();
                }
                catch (Exception)
                {
                    Debug.LogFormat("Cannot delete file: ", file.Name);
                }
            } 

            // Subscribing to the Microsoft HoloLens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();
        }
    ```

7.  <span data-ttu-id="242b4-383">Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit:</span><span class="sxs-lookup"><span data-stu-id="242b4-383">Implement a handler that will be called when a Tap gesture occurs:</span></span>

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            if (!captureIsActive)
            {
                captureIsActive = true;

                // Set the cursor color to red
                SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;

                // Begin the capture loop
                Invoke("ExecuteImageCaptureAndAnalysis", 0);
            }
        }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="242b4-384">Lorsque le curseur est **vert**, cela signifie que l’appareil photo est disponible pour prendre l’image.</span><span class="sxs-lookup"><span data-stu-id="242b4-384">When the cursor is **green**, it means the camera is available to take the image.</span></span> <span data-ttu-id="242b4-385">Lorsque le curseur est **rouge**, cela signifie que l’appareil photo est occupé.</span><span class="sxs-lookup"><span data-stu-id="242b4-385">When the cursor is **red**, it means the camera is busy.</span></span>

8.  <span data-ttu-id="242b4-386">Ajoutez la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image:</span><span class="sxs-lookup"><span data-stu-id="242b4-386">Add the method that the application uses to start the image capture process and store the image:</span></span>

    ```csharp
        /// <summary>
        /// Begin process of image capturing and send to Azure Custom Vision Service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            // Create a label in world space using the ResultsLabel class 
            // Invisible at this point but correctly positioned where the image was taken
            SceneOrganiser.Instance.PlaceAnalysisLabel();

            // Set the camera resolution to be the highest possible
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending
                ((res) => res.width * res.height).First();
            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            // Begin capture process, set the image format
            PhotoCapture.CreateAsync(true, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters camParameters = new CameraParameters
                {
                    hologramOpacity = 1.0f,
                    cameraResolutionWidth = targetTexture.width,
                    cameraResolutionHeight = targetTexture.height,
                    pixelFormat = CapturePixelFormat.BGRA32
                };

                // Capture the image from the camera and save it in the App internal folder
                captureObject.StartPhotoModeAsync(camParameters, delegate (PhotoCapture.PhotoCaptureResult result)
                {
                    string filename = string.Format(@"CapturedImage{0}.jpg", captureCount);
                    filePath = Path.Combine(Application.persistentDataPath, filename);          
                    captureCount++;              
                    photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);              
                });
            });
        }
    ```

9.  <span data-ttu-id="242b4-387">Ajoutez les gestionnaires qui seront appelés lorsque la photo a été capturée et le moment où elle sera prête à être analysée.</span><span class="sxs-lookup"><span data-stu-id="242b4-387">Add the handlers that will be called when the photo has been captured and for when it is ready to be analyzed.</span></span> <span data-ttu-id="242b4-388">Le résultat est ensuite transmis à **CustomVisionAnalyser** pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="242b4-388">The result is then passed to the **CustomVisionAnalyser** for analysis.</span></span>

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. 
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
            try
            {
                // Call StopPhotoMode once the image has successfully captured
                photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
            }
            catch (Exception e)
            {
                Debug.LogFormat("Exception capturing photo to disk: {0}", e.Message);
            }
        }

        /// <summary>
        /// The camera photo mode has stopped after the capture.
        /// Begin the image analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            Debug.LogFormat("Stopped Photo Mode");
        
            // Dispose from the object in memory and request the image analysis 
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            // Call the image analysis
            StartCoroutine(CustomVisionAnalyser.Instance.AnalyseLastImageCaptured(filePath)); 
        }

        /// <summary>
        /// Stops all capture pending actions
        /// </summary>
        internal void ResetImageCapture()
        {
            captureIsActive = false;

            // Set the cursor color to green
            SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.green;

            // Stop the capture loop if active
            CancelInvoke();
        }
    ```

10. <span data-ttu-id="242b4-389">Veillez à enregistrer vos modifications dans **Visual Studio**avant de revenir à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="242b4-389">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-11---setting-up-the-scripts-in-the-scene"></a><span data-ttu-id="242b4-390">Chapitre 11-configuration des scripts dans la scène</span><span class="sxs-lookup"><span data-stu-id="242b4-390">Chapter 11 - Setting up the scripts in the scene</span></span>

<span data-ttu-id="242b4-391">Maintenant que vous avez écrit l’ensemble du code nécessaire pour ce projet, il est temps de configurer les scripts dans la scène et, sur le prefabs, pour qu’ils se comportent correctement.</span><span class="sxs-lookup"><span data-stu-id="242b4-391">Now that you have written all of the code necessary for this project, is time to set up the scripts in the scene, and on the prefabs, for them to behave correctly.</span></span>

1.  <span data-ttu-id="242b4-392">Dans l' **éditeur Unity**, dans le **panneau hiérarchie**, sélectionnez l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="242b4-392">Within the **Unity Editor**, in the **Hierarchy Panel**, select the **Main Camera**.</span></span>
2.  <span data-ttu-id="242b4-393">Dans le **panneau Inspecteur**, avec l' **appareil photo principal** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **SceneOrganiser** et double-cliquez dessus pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="242b4-393">In the **Inspector Panel**, with the **Main Camera** selected, click on **Add Component**, then search for **SceneOrganiser** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-38.png)

3.  <span data-ttu-id="242b4-394">Dans le **panneau Projet**, ouvrez le **dossier Prefabs**, faites glisser l' **étiquette** Prefab dans la zone d’entrée cible de référence de l' *étiquette* vide, dans le script **SceneOrganiser** que vous venez d’ajouter à la *caméra principale*, comme illustré dans l’image ci-dessous:</span><span class="sxs-lookup"><span data-stu-id="242b4-394">In the **Project Panel**, open the **Prefabs folder**, drag the **Label** prefab into the *Label* empty reference target input area, in the **SceneOrganiser** script that you have just added to the *Main Camera*, as shown in the image below:</span></span>

    ![](images/AzureLabs-Lab310-39.png)

4.  <span data-ttu-id="242b4-395">Dans le **volet hiérarchie**, sélectionnez l’enfant **GazeCursor** de l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="242b4-395">In the **Hierarchy Panel**, select the **GazeCursor** child of the **Main Camera**.</span></span>
5.  <span data-ttu-id="242b4-396">Dans le **volet**de l’inspecteur, avec le **GazeCursor** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **GazeCursor** et double-cliquez dessus pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="242b4-396">In the **Inspector Panel**, with the **GazeCursor** selected, click on **Add Component**, then search for **GazeCursor** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-40.png)

6.  <span data-ttu-id="242b4-397">Là encore, dans le **panneau hiérarchie**, sélectionnez l’enfant **SpatialMapping** de l' **appareil photo principal**.</span><span class="sxs-lookup"><span data-stu-id="242b4-397">Again, in the **Hierarchy Panel**, select the **SpatialMapping** child of the **Main Camera**.</span></span>
7.  <span data-ttu-id="242b4-398">Dans le **volet**de l’inspecteur, avec le **SpatialMapping** sélectionné, cliquez sur **Ajouter un composant**, puis recherchez le script **SpatialMapping** et double-cliquez dessus pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="242b4-398">In the **Inspector Panel**, with the **SpatialMapping** selected, click on **Add Component**, then search for **SpatialMapping** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-41.png)

<span data-ttu-id="242b4-399">Les scripts restants que vous n’avez pas définis seront ajoutés par le code dans le script **SceneOrganiser** , pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="242b4-399">The remaining scripts thats you have not set will be added by the code in the **SceneOrganiser** script, during runtime.</span></span>

## <a name="chapter-12---before-building"></a><span data-ttu-id="242b4-400">Chapitre 12-avant génération</span><span class="sxs-lookup"><span data-stu-id="242b4-400">Chapter 12 - Before building</span></span>

<span data-ttu-id="242b4-401">Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="242b4-401">To perform a thorough test of your application you will need to sideload it onto your Microsoft HoloLens.</span></span>

<span data-ttu-id="242b4-402">Avant cela, assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="242b4-402">Before you do, ensure that:</span></span>

-  <span data-ttu-id="242b4-403">Tous les paramètres mentionnés dans le [chapitre 3](#chapter-3---set-up-the-unity-project) sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="242b4-403">All the settings mentioned in the [Chapter 3](#chapter-3---set-up-the-unity-project) are set correctly.</span></span>
- <span data-ttu-id="242b4-404">Le script **SceneOrganiser** est attaché à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="242b4-404">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span>
- <span data-ttu-id="242b4-405">Le script **GazeCursor** est attaché à l’objet **GazeCursor** .</span><span class="sxs-lookup"><span data-stu-id="242b4-405">The script **GazeCursor** is attached to the **GazeCursor** object.</span></span>
- <span data-ttu-id="242b4-406">Le script **SpatialMapping** est attaché à l’objet **SpatialMapping** .</span><span class="sxs-lookup"><span data-stu-id="242b4-406">The script **SpatialMapping** is attached to the **SpatialMapping** object.</span></span>
- <span data-ttu-id="242b4-407">Dans le [Chapitre 5](#chapter-5---create-the-customvisionanalyser-class), étape 6:</span><span class="sxs-lookup"><span data-stu-id="242b4-407">In [Chapter 5](#chapter-5---create-the-customvisionanalyser-class), Step 6:</span></span>

    - <span data-ttu-id="242b4-408">Veillez à insérer votre **clé** de prédiction de service dans la variable **predictionKey** .</span><span class="sxs-lookup"><span data-stu-id="242b4-408">Make sure you insert your **Service Prediction Key** into the **predictionKey** variable.</span></span>
    - <span data-ttu-id="242b4-409">Vous avez inséré votre **point de terminaison** de prédiction dans la classe **predictionEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="242b4-409">You have inserted your **Prediction Endpoint** into the **predictionEndpoint** class.</span></span>

## <a name="chapter-13---build-the-uwp-solution-and-sideload-your-application"></a><span data-ttu-id="242b4-410">Chapitre 13: créer la solution UWP et chargement votre application</span><span class="sxs-lookup"><span data-stu-id="242b4-410">Chapter 13 - Build the UWP solution and sideload your application</span></span>

<span data-ttu-id="242b4-411">Vous êtes maintenant prêt à créer votre application en tant que solution UWP que vous pourrez déployer sur Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="242b4-411">You are now ready to build you application as a UWP Solution that you will be able to deploy on to the Microsoft HoloLens.</span></span> <span data-ttu-id="242b4-412">Pour commencer le processus de génération:</span><span class="sxs-lookup"><span data-stu-id="242b4-412">To begin the build process:</span></span>

1.  <span data-ttu-id="242b4-413">Accédez à **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="242b4-413">Go to **File > Build Settings**.</span></span>

2.  <span data-ttu-id="242b4-414">**Projets Tick Unity C\#** .</span><span class="sxs-lookup"><span data-stu-id="242b4-414">Tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="242b4-415">Cliquez sur **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="242b4-415">Click on **Add Open Scenes**.</span></span> <span data-ttu-id="242b4-416">Cette opération ajoute la scène actuellement ouverte à la Build.</span><span class="sxs-lookup"><span data-stu-id="242b4-416">This will add the currently open scene to the build.</span></span>

    ![](images/AzureLabs-Lab310-42.png)

4.  <span data-ttu-id="242b4-417">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="242b4-417">Click **Build**.</span></span> <span data-ttu-id="242b4-418">Unity lance une fenêtre de l' *Explorateur de fichiers* , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="242b4-418">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="242b4-419">Créez ce dossier maintenant, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="242b4-419">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="242b4-420">Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="242b4-420">Then with the **App** folder selected, click **Select Folder**.</span></span>

5.  <span data-ttu-id="242b4-421">Unity commence à générer votre projet dans le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="242b4-421">Unity will begin building your project to the **App** folder.</span></span>

6.  <span data-ttu-id="242b4-422">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="242b4-422">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

7.  <span data-ttu-id="242b4-423">Pour effectuer un déploiement sur Microsoft HoloLens, vous aurez besoin de l’adresse IP de cet appareil (pour le déploiement à distance) et pour vous assurer qu’il est également défini **en mode développeur** .</span><span class="sxs-lookup"><span data-stu-id="242b4-423">To deploy on to Microsoft HoloLens, you will need the IP Address of that device (for Remote Deploy), and to ensure that it also has **Developer Mode** set.</span></span> <span data-ttu-id="242b4-424">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="242b4-424">To do this:</span></span>

    1.  <span data-ttu-id="242b4-425">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="242b4-425">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="242b4-426">Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet</span><span class="sxs-lookup"><span data-stu-id="242b4-426">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="242b4-427">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="242b4-427">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="242b4-428">Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="242b4-428">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="242b4-429">Définissez le **mode développeur** *sur*.</span><span class="sxs-lookup"><span data-stu-id="242b4-429">Set **Developer Mode** *On*.</span></span>

8.  <span data-ttu-id="242b4-430">Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="242b4-430">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

9.  <span data-ttu-id="242b4-431">Dans la configuration de lasolution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="242b4-431">In the Solution Configuration select **Debug**.</span></span>

10. <span data-ttu-id="242b4-432">Dans la plateforme de la solution, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="242b4-432">In the Solution Platform, select **x86, Remote Machine**.</span></span> <span data-ttu-id="242b4-433">Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le Microsoft HoloLens, dans ce cas, que vous avez noté).</span><span class="sxs-lookup"><span data-stu-id="242b4-433">You will be prompted to insert the **IP address** of a remote device (the Microsoft HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab310-43.png)

11. <span data-ttu-id="242b4-434">Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="242b4-434">Go to the **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

12. <span data-ttu-id="242b4-435">Votre application doit maintenant apparaître dans la liste des applications installées sur votre Microsoft HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="242b4-435">Your app should now appear in the list of installed apps on your Microsoft HoloLens, ready to be launched!</span></span>

### <a name="to-use-the-application"></a><span data-ttu-id="242b4-436">Pour utiliser l’application:</span><span class="sxs-lookup"><span data-stu-id="242b4-436">To use the application:</span></span>

* <span data-ttu-id="242b4-437">Examinez un objet, que vous avez formé avec votre **service vision personnalisée Azure, la détection d’objets**et utilisez le **geste TAP**.</span><span class="sxs-lookup"><span data-stu-id="242b4-437">Look at an object, which you have trained with your **Azure Custom Vision Service, Object Detection**, and use the **Tap gesture**.</span></span>
* <span data-ttu-id="242b4-438">Si l’objet est correctement détecté, un *texte d’étiquette* de l’espace universel apparaît avec le nom de la balise.</span><span class="sxs-lookup"><span data-stu-id="242b4-438">If the object is successfully detected, a world-space *Label Text* will appear with the tag name.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="242b4-439">Chaque fois que vous capturez une photo et que vous l’envoyez au service, vous pouvez revenir à la page du service et reformer le service avec les images nouvellement capturées.</span><span class="sxs-lookup"><span data-stu-id="242b4-439">Every time you capture a photo and send it to the Service, you can go back to the Service page and retrain the Service with the newly captured images.</span></span> <span data-ttu-id="242b4-440">Au début, vous devrez probablement corriger les *zones englobantes* pour qu’elles soient plus précises et reformer le service.</span><span class="sxs-lookup"><span data-stu-id="242b4-440">At the beginning, you will probably also have to correct the *Bounding Boxes* to be more accurate and retrain the Service.</span></span>

> [!NOTE]
> <span data-ttu-id="242b4-441">Le texte de l’étiquette placée peut ne pas apparaître près de l’objet lorsque les capteurs Microsoft HoloLens et/ou SpatialTrackingComponent dans Unity ne peuvent pas placer les conflits appropriés, par rapport aux objets réels.</span><span class="sxs-lookup"><span data-stu-id="242b4-441">The Label Text placed might not appear near the object when the Microsoft HoloLens sensors and/or the SpatialTrackingComponent in Unity fails to place the appropriate colliders, relative to the real world objects.</span></span> <span data-ttu-id="242b4-442">Si c’est le cas, essayez d’utiliser l’application sur une autre surface.</span><span class="sxs-lookup"><span data-stu-id="242b4-442">Try to use the application on a different surface if that is the case.</span></span>

## <a name="your-custom-vision-object-detection-application"></a><span data-ttu-id="242b4-443">Votre Custom Vision, application de détection d’objets</span><span class="sxs-lookup"><span data-stu-id="242b4-443">Your Custom Vision, Object Detection application</span></span>

<span data-ttu-id="242b4-444">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de détection d’objets Azure Custom Vision, qui peut reconnaître un objet d’une image, puis fournir une position approximative pour cet objet dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="242b4-444">Congratulations, you built a mixed reality app that leverages the Azure Custom Vision, Object Detection API, which can recognize an object from an image, and then provide an approximate position for that object in 3D space.</span></span>

![](images/AzureLabs-Lab310-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="242b4-445">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="242b4-445">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="242b4-446">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="242b4-446">Exercise 1</span></span>

<span data-ttu-id="242b4-447">En ajoutant à l’étiquette de texte, utilisez un cube semi-transparent pour encapsuler l’objet réel dans un *rectangle englobant*3D.</span><span class="sxs-lookup"><span data-stu-id="242b4-447">Adding to the Text Label, use a semi-transparent cube to wrap the real object in a 3D *Bounding Box*.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="242b4-448">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="242b4-448">Exercise 2</span></span>

<span data-ttu-id="242b4-449">Formez votre Service Vision personnalisée pour qu’il reconnaisse plus d’objets.</span><span class="sxs-lookup"><span data-stu-id="242b4-449">Train your Custom Vision Service to recognize more objects.</span></span>

### <a name="exercise-3"></a><span data-ttu-id="242b4-450">Exercice 3</span><span class="sxs-lookup"><span data-stu-id="242b4-450">Exercise 3</span></span>

<span data-ttu-id="242b4-451">Émettre un signal sonore lorsqu’un objet est reconnu.</span><span class="sxs-lookup"><span data-stu-id="242b4-451">Play a sound when an object is recognized.</span></span>

### <a name="exercise-4"></a><span data-ttu-id="242b4-452">Exercice 4</span><span class="sxs-lookup"><span data-stu-id="242b4-452">Exercise 4</span></span>

<span data-ttu-id="242b4-453">Utilisez l’API pour reformer votre service avec les mêmes images que celles que votre application analyse, afin de rendre le service plus précis (effectuer la prédiction et la formation simultanément).</span><span class="sxs-lookup"><span data-stu-id="242b4-453">Use the API to re-train your Service with the same images your app is analyzing, so to make the Service more accurate (do both prediction and training simultaneously).</span></span>
