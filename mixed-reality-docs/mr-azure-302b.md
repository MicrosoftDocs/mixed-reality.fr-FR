---
title: MR et Azure 302b-vision personnalisée
description: Suivez ce cours pour apprendre à former un modèle de Machine Learning, puis à utiliser le modèle formé pour reconnaître des objets similaires dans une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/03/2018
ms.topic: article
keywords: Azure, réalité mixte, Academy, Unity, didacticiel, API, vision personnalisée, hololens, immersif, VR
ms.openlocfilehash: e6e9782a8d559af660dc4765556f1e926c5360b1
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63553607"
---
>[!NOTE]
><span data-ttu-id="73331-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="73331-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="73331-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="73331-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="73331-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="73331-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="73331-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="73331-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="73331-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="73331-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="73331-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="73331-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-302b-custom-vision"></a><span data-ttu-id="73331-110">RM et Azure 302b: Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="73331-110">MR and Azure 302b: Custom vision</span></span>

<span data-ttu-id="73331-111">Dans ce cours, vous allez apprendre à reconnaître du contenu visuel personnalisé dans une image fournie, à l’aide des fonctionnalités d’Azure Custom Vision dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="73331-111">In this course, you will learn how to recognize custom visual content within a provided image, using Azure Custom Vision capabilities in a mixed reality application.</span></span>

<span data-ttu-id="73331-112">Ce service vous permet d’effectuer l’apprentissage d’un modèle de Machine Learning à l’aide d’images d’objet.</span><span class="sxs-lookup"><span data-stu-id="73331-112">This service will allow you to train a machine learning model using object images.</span></span> <span data-ttu-id="73331-113">Vous utiliserez ensuite le modèle formé pour reconnaître des objets similaires, fournis par la capture de l’appareil photo de Microsoft HoloLens ou un appareil photo connecté à votre PC pour les casques immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="73331-113">You will then use the trained model to recognize similar objects, as provided by the camera capture of Microsoft HoloLens or a camera connected to your PC for immersive (VR) headsets.</span></span>

![résultat du cours](images/AzureLabs-Lab302b-00.png)

<span data-ttu-id="73331-115">Azure Custom Vision est un service cognitive de Microsoft qui permet aux développeurs de créer des classifieurs d’images personnalisées.</span><span class="sxs-lookup"><span data-stu-id="73331-115">Azure Custom Vision is a Microsoft Cognitive Service which allows developers to build custom image classifiers.</span></span> <span data-ttu-id="73331-116">Ces classifieurs peuvent ensuite être utilisés avec de nouvelles images pour reconnaître, ou classer, des objets dans cette nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="73331-116">These classifiers can then be used with new images to recognize, or classify, objects within that new image.</span></span> <span data-ttu-id="73331-117">Le service fournit un portail en ligne simple et facile à utiliser pour simplifier le processus.</span><span class="sxs-lookup"><span data-stu-id="73331-117">The Service provides a simple, easy to use, online portal to streamline the process.</span></span> <span data-ttu-id="73331-118">Pour plus d’informations, consultez la [page service vision personnalisée Azure](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span><span class="sxs-lookup"><span data-stu-id="73331-118">For more information, visit the [Azure Custom Vision Service page](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span></span>

<span data-ttu-id="73331-119">À la fin de ce cours, vous disposerez d’une application de réalité mixte qui pourra fonctionner en deux modes:</span><span class="sxs-lookup"><span data-stu-id="73331-119">Upon completion of this course, you will have a mixed reality application which will be able to work in two modes:</span></span>

-   <span data-ttu-id="73331-120">**Mode d’analyse**: configuration manuelle du service vision personnalisée en chargeant des images, en créant des balises et en formant une formation au service pour reconnaître différents objets (dans ce cas, la souris et le clavier).</span><span class="sxs-lookup"><span data-stu-id="73331-120">**Analysis Mode**: setting up the Custom Vision Service manually by uploading images, creating tags, and training the Service to recognize different objects (in this case mouse and keyboard).</span></span> <span data-ttu-id="73331-121">Vous allez ensuite créer une application HoloLens qui capturera les images à l’aide de l’appareil photo et essayez de reconnaître ces objets dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="73331-121">You will then create a HoloLens app that will capture images using the camera, and try to recognize those objects in the real world.</span></span>

-   <span data-ttu-id="73331-122">**Mode d’apprentissage**: vous allez implémenter le code qui activera un «mode d’apprentissage» dans votre application.</span><span class="sxs-lookup"><span data-stu-id="73331-122">**Training Mode**: you will implement code that will enable a "Training Mode" in your app.</span></span> <span data-ttu-id="73331-123">Le mode d’apprentissage vous permet de capturer des images à l’aide de l’appareil photo HoloLens, de charger les images capturées dans le service et d’effectuer l’apprentissage du modèle de vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="73331-123">The training mode will allow you to capture images using the HoloLens' camera, upload the captured images to the Service, and train the custom vision model.</span></span>

<span data-ttu-id="73331-124">Ce cours vous apprend à obtenir les résultats de la Service Vision personnalisée dans un exemple d’application basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-124">This course will teach you how to get the results from the Custom Vision Service into a Unity-based sample application.</span></span> <span data-ttu-id="73331-125">Il vous faudra appliquer ces concepts à une application personnalisée que vous pouvez générer.</span><span class="sxs-lookup"><span data-stu-id="73331-125">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="73331-126">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="73331-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="73331-127">Course</span><span class="sxs-lookup"><span data-stu-id="73331-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="73331-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="73331-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="73331-129"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="73331-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="73331-130">RM et Azure 302b: Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="73331-130">MR and Azure 302b: Custom vision</span></span></td><td style="text-align: center;"> <span data-ttu-id="73331-131">✔️</span><span class="sxs-lookup"><span data-stu-id="73331-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="73331-132">✔️</span><span class="sxs-lookup"><span data-stu-id="73331-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="73331-133">Bien que ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques pour Windows Mixed Reality (VR).</span><span class="sxs-lookup"><span data-stu-id="73331-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="73331-134">Étant donné que les casques immersifs ne disposent pas de caméras accessibles, vous aurez besoin d’une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="73331-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="73331-135">À mesure que vous suivez le cours, vous verrez des remarques sur les modifications que vous devrez peut-être utiliser pour prendre en charge les écouteurs immersifs (VR).</span><span class="sxs-lookup"><span data-stu-id="73331-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="73331-136">Prérequis</span><span class="sxs-lookup"><span data-stu-id="73331-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="73331-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base C#avec Unity et.</span><span class="sxs-lookup"><span data-stu-id="73331-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="73331-138">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="73331-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="73331-139">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="73331-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="73331-140">Nous vous recommandons d’utiliser le matériel et les logiciels suivants pour ce cours:</span><span class="sxs-lookup"><span data-stu-id="73331-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="73331-141">Un PC de développement, [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement d’écouteurs immersif (VR)</span><span class="sxs-lookup"><span data-stu-id="73331-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="73331-142">Windows 10 automne Creators Update (ou version ultérieure) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="73331-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="73331-143">Le dernier Kit de développement logiciel Windows 10</span><span class="sxs-lookup"><span data-stu-id="73331-143">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="73331-144">Unity 2017,4</span><span class="sxs-lookup"><span data-stu-id="73331-144">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="73331-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="73331-145">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="73331-146">Un [casque Windows Mixed Reality (VR)](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur activé</span><span class="sxs-lookup"><span data-stu-id="73331-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="73331-147">Appareil photo connecté à votre PC (pour le développement d’un casque immersif)</span><span class="sxs-lookup"><span data-stu-id="73331-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="73331-148">Accès à Internet pour l’installation d’Azure et la récupération de l’API Custom Vision</span><span class="sxs-lookup"><span data-stu-id="73331-148">Internet access for Azure setup and Custom Vision API retrieval</span></span>
- <span data-ttu-id="73331-149">Une série d’au moins cinq (5) images (dix (10) recommandé) pour chaque objet que vous souhaitez que le Service Vision personnalisée reconnaître.</span><span class="sxs-lookup"><span data-stu-id="73331-149">A series of at least five (5) images (ten (10) recommended) for each object that you would like the Custom Vision Service to recognize.</span></span> <span data-ttu-id="73331-150">Si vous le souhaitez, vous pouvez utiliser [les images déjà fournies dans ce cours (une souris d’ordinateur et un clavier) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span><span class="sxs-lookup"><span data-stu-id="73331-150">If you wish, you can use [the images already provided with this course (a computer mouse and a keyboard) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="73331-151">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="73331-151">Before you start</span></span>

1.  <span data-ttu-id="73331-152">Pour éviter de rencontrer des problèmes lors de la création de ce projet, il est fortement recommandé de créer le projet mentionné dans ce didacticiel dans un dossier racine ou dans un dossier racine (les chemins de dossiers longs peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="73331-152">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="73331-153">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="73331-153">Set up and test your HoloLens.</span></span> <span data-ttu-id="73331-154">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="73331-154">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="73331-155">Il est judicieux d’effectuer un réglage de l’étalonnage et du capteur au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="73331-155">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="73331-156">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="73331-156">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="73331-157">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="73331-157">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-custom-vision-service-portal"></a><span data-ttu-id="73331-158">Chapitre 1-portail Service Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="73331-158">Chapter 1 - The Custom Vision Service Portal</span></span>

<span data-ttu-id="73331-159">Pour utiliser le *service vision personnalisée* dans Azure, vous devez configurer une instance du service qui sera mise à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="73331-159">To use the *Custom Vision Service* in Azure, you will need to configure an instance of the Service to be made available to your application.</span></span>

1.  <span data-ttu-id="73331-160">Tout d’abord, [accédez à la page principale *service vision personnalisée* ](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span><span class="sxs-lookup"><span data-stu-id="73331-160">First, [navigate to the *Custom Vision Service* main page](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span></span>

2.  <span data-ttu-id="73331-161">Cliquez sur le bouton **prise en main** .</span><span class="sxs-lookup"><span data-stu-id="73331-161">Click on the **Get Started** button.</span></span>

    ![](images/AzureLabs-Lab302b-01.png)

3.  <span data-ttu-id="73331-162">Connectez-vous au portail *service vision personnalisée* .</span><span class="sxs-lookup"><span data-stu-id="73331-162">Sign in to the *Custom Vision Service* Portal.</span></span>

    ![](images/AzureLabs-Lab302b-02.png)

    > [!NOTE]
    > <span data-ttu-id="73331-163">Si vous n’avez pas encore de compte Azure, vous devez en créer un.</span><span class="sxs-lookup"><span data-stu-id="73331-163">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="73331-164">Si vous suivez ce didacticiel dans une situation de classe ou de laboratoire, demandez à votre formateur ou à l’un des prostructors de vous aider à configurer votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="73331-164">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

4.  <span data-ttu-id="73331-165">Une fois que vous êtes connecté pour la première fois, vous êtes invité à entrer dans le panneau *des conditions d’accès* .</span><span class="sxs-lookup"><span data-stu-id="73331-165">Once you are logged in for the first time, you will be prompted with the *Terms of Service* panel.</span></span> <span data-ttu-id="73331-166">Cliquez sur la case à cocher pour accepter les termes du contrat.</span><span class="sxs-lookup"><span data-stu-id="73331-166">Click on the checkbox to agree to the terms.</span></span> <span data-ttu-id="73331-167">Cliquez ensuite sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="73331-167">Then click on **I agree**.</span></span>

    ![](images/AzureLabs-Lab302b-03.png)

5.  <span data-ttu-id="73331-168">Une fois les conditions accordées, vous accédez à la section *projets* du portail.</span><span class="sxs-lookup"><span data-stu-id="73331-168">Having agreed to the Terms, you will be navigated to the *Projects* section of the Portal.</span></span> <span data-ttu-id="73331-169">Cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="73331-169">Click on **New Project**.</span></span>

    ![](images/AzureLabs-Lab302b-04.png)

6.  <span data-ttu-id="73331-170">Un onglet s’affiche sur le côté droit, ce qui vous invite à spécifier certains champs pour le projet.</span><span class="sxs-lookup"><span data-stu-id="73331-170">A tab will appear on the right-hand side, which will prompt you to specify some fields for the project.</span></span>

    1.  <span data-ttu-id="73331-171">Insérez un *nom* pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="73331-171">Insert a *Name* for your project.</span></span>

    2.  <span data-ttu-id="73331-172">Insérez une *Description* de votre projet (*facultatif*).</span><span class="sxs-lookup"><span data-stu-id="73331-172">Insert a *Description* for your project (*optional*).</span></span>

    3.  <span data-ttu-id="73331-173">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="73331-173">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="73331-174">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="73331-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="73331-175">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="73331-175">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

    4. <span data-ttu-id="73331-176">Définir les *types de projets* sur **classification**</span><span class="sxs-lookup"><span data-stu-id="73331-176">Set the *Project Types* to **Classification**</span></span>
    
    5. <span data-ttu-id="73331-177">Définissez les *domaines* comme étant **généraux**.</span><span class="sxs-lookup"><span data-stu-id="73331-177">Set the *Domains* as **General**.</span></span>

        ![](images/AzureLabs-Lab302b-05.png)

        > <span data-ttu-id="73331-178">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, consultez [l’article du groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="73331-178">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

7.  <span data-ttu-id="73331-179">Une fois que vous avez terminé, cliquez sur **créer un projet**, vous serez redirigé vers la page service vision personnalisée, projet.</span><span class="sxs-lookup"><span data-stu-id="73331-179">Once you are finished, click on **Create project**, you will be redirected to the Custom Vision Service, project page.</span></span>

## <a name="chapter-2---training-your-custom-vision-project"></a><span data-ttu-id="73331-180">Chapitre 2-formation de votre projet Custom Vision</span><span class="sxs-lookup"><span data-stu-id="73331-180">Chapter 2 - Training your Custom Vision project</span></span>

<span data-ttu-id="73331-181">Une fois dans le portail Custom Vision, votre objectif principal est de former votre projet à la reconnaissance d’objets spécifiques dans les images.</span><span class="sxs-lookup"><span data-stu-id="73331-181">Once in the Custom Vision portal, your primary objective is to train your project to recognize specific objects in images.</span></span> <span data-ttu-id="73331-182">Vous avez besoin d’au moins cinq (5) images, même si dix (10) sont préférables pour chaque objet que vous souhaitez que votre application reconnaisse.</span><span class="sxs-lookup"><span data-stu-id="73331-182">You need at least five (5) images, though ten (10) is preferred, for each object that you would like your application to recognize.</span></span> <span data-ttu-id="73331-183">[Vous pouvez utiliser les images fournies dans ce cours (une souris d’ordinateur et un clavier)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span><span class="sxs-lookup"><span data-stu-id="73331-183">[You can use the images provided with this course (a computer mouse and a keyboard)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span></span> 

<span data-ttu-id="73331-184">Pour former votre projet Service Vision personnalisée:</span><span class="sxs-lookup"><span data-stu-id="73331-184">To train your Custom Vision Service project:</span></span>

1.  <span data-ttu-id="73331-185">Cliquez sur le **+** bouton en regard de **balises.**</span><span class="sxs-lookup"><span data-stu-id="73331-185">Click on the **+** button next to **Tags.**</span></span>

    ![](images/AzureLabs-Lab302b-06.png)

2.  <span data-ttu-id="73331-186">Ajoutez le **nom** de l’objet que vous souhaitez reconnaître.</span><span class="sxs-lookup"><span data-stu-id="73331-186">Add the **name** of the object you would like to recognize.</span></span> <span data-ttu-id="73331-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="73331-187">Click on **Save**.</span></span>

    ![](images/AzureLabs-Lab302b-07.png)

3.  <span data-ttu-id="73331-188">Vous remarquerez  que votre balise a été ajoutée (vous devrez peut-être recharger votre page pour qu’elle apparaisse).</span><span class="sxs-lookup"><span data-stu-id="73331-188">You will notice your **Tag** has been added (you may need to reload your page for it to appear).</span></span> <span data-ttu-id="73331-189">Cliquez sur la case à cocher en regard de votre nouvelle balise, si elle n’est pas déjà activée.</span><span class="sxs-lookup"><span data-stu-id="73331-189">Click the checkbox alongside your new tag, if it is not already checked.</span></span>

    ![](images/AzureLabs-Lab302b-08.png)

4.  <span data-ttu-id="73331-190">Cliquez sur **Ajouter des images** au centre de la page.</span><span class="sxs-lookup"><span data-stu-id="73331-190">Click on **Add Images** in the center of the page.</span></span>

    ![](images/AzureLabs-Lab302b-09.png)

5.  <span data-ttu-id="73331-191">Cliquez sur **Parcourir les fichiers locaux**et recherchez, puis sélectionnez les images que vous souhaitez télécharger, avec un minimum de cinq (5).</span><span class="sxs-lookup"><span data-stu-id="73331-191">Click on **Browse local files**, and search, then select, the images you would like to upload, with the minimum being five (5).</span></span> <span data-ttu-id="73331-192">N’oubliez pas que toutes ces images doivent contenir l’objet que vous êtes en train de former.</span><span class="sxs-lookup"><span data-stu-id="73331-192">Remember all of these images should contain the object which you are training.</span></span>

    > [!NOTE]
    >  <span data-ttu-id="73331-193">Vous pouvez sélectionner plusieurs images à la fois, à télécharger.</span><span class="sxs-lookup"><span data-stu-id="73331-193">You can select several images at a time, to upload.</span></span>

6.  <span data-ttu-id="73331-194">Une fois que vous pouvez voir les images dans l’onglet, sélectionnez la balise appropriée dans la zone **mes balises** .</span><span class="sxs-lookup"><span data-stu-id="73331-194">Once you can see the images in the tab, select the appropriate tag in the **My Tags** box.</span></span>

    ![](images/AzureLabs-Lab302b-10.png)

7.  <span data-ttu-id="73331-195">Cliquez sur **charger les fichiers**.</span><span class="sxs-lookup"><span data-stu-id="73331-195">Click on **Upload files**.</span></span> <span data-ttu-id="73331-196">Le chargement des fichiers va commencer.</span><span class="sxs-lookup"><span data-stu-id="73331-196">The files will begin uploading.</span></span> <span data-ttu-id="73331-197">Une fois que vous avez confirmé le téléchargement, cliquez sur **terminé**.</span><span class="sxs-lookup"><span data-stu-id="73331-197">Once you have confirmation of the upload, click **Done**.</span></span>

    ![](images/AzureLabs-Lab302b-11.png)

8.  <span data-ttu-id="73331-198">Répétez le même processus pour créer une  nouvelle balise nommée **Keyboard** et chargez les photos appropriées pour celle-ci.</span><span class="sxs-lookup"><span data-stu-id="73331-198">Repeat the same process to create a new **Tag** named **Keyboard** and upload the appropriate photos for it.</span></span> <span data-ttu-id="73331-199">Veillez à ne pas **vérifier** la *souris* une fois que vous avez créé les nouvelles balises, afin d’afficher la fenêtre *Ajouter des images* .</span><span class="sxs-lookup"><span data-stu-id="73331-199">Make sure to **uncheck** *Mouse* once you have created the new tags, so to show the *Add images* window.</span></span>

9.  <span data-ttu-id="73331-200">Une fois que les deux balises sont configurées, cliquez sur **train**, et la première itération d’apprentissage commencera la génération.</span><span class="sxs-lookup"><span data-stu-id="73331-200">Once you have both Tags set up, click on **Train**, and the first training iteration will start building.</span></span>

    ![](images/AzureLabs-Lab302b-12.png)

10. <span data-ttu-id="73331-201">Une fois qu’elle est créée, vous pouvez voir deux boutons nommés **créer par défaut** et **URL**de prédiction.</span><span class="sxs-lookup"><span data-stu-id="73331-201">Once it is built, you will be able to see two buttons called **Make default** and **Prediction URL**.</span></span> <span data-ttu-id="73331-202">Cliquez d’abord sur **créer par défaut** , puis sur **URL**de prédiction.</span><span class="sxs-lookup"><span data-stu-id="73331-202">Click on **Make default** first, then click on **Prediction URL**.</span></span>

    ![](images/AzureLabs-Lab302b-13.png)

    > [!NOTE] 
    > <span data-ttu-id="73331-203">L’URL du point de terminaison qui est fournie à partir de ce, est définie sur l' *itération* qui a été marquée comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="73331-203">The endpoint URL which is provided from this, is set to whichever *Iteration* has been marked as default.</span></span> <span data-ttu-id="73331-204">Par conséquent, si vous effectuez ultérieurement une nouvelle *itération* et la mettez à jour par défaut, vous n’aurez pas besoin de modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="73331-204">As such, if you later make a new *Iteration* and update it as default, you will not need to change your code.</span></span>

11. <span data-ttu-id="73331-205">Une fois que vous avez cliqué sur *URL*de prédiction, ouvrez *le bloc-notes*, puis copiez et collez l' **URL** et la clé de prédiction, afin de pouvoir la récupérer lorsque vous en aurez besoin ultérieurement dans le code.</span><span class="sxs-lookup"><span data-stu-id="73331-205">Once you have clicked on *Prediction URL*, open *Notepad*, and copy and paste the **URL** and the **Prediction-Key**, so that you can retrieve it when you need it later in the code.</span></span>

    ![](images/AzureLabs-Lab302b-14.png)

12. <span data-ttu-id="73331-206">Cliquez sur le **roue dentée** en haut à droite de l’écran.</span><span class="sxs-lookup"><span data-stu-id="73331-206">Click on the **Cog** at the top right of the screen.</span></span>

    ![](images/AzureLabs-Lab302b-15.png)

13. <span data-ttu-id="73331-207">Copiez la **clé de formation** et collez-la dans un *bloc-notes*, pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="73331-207">Copy the **Training Key** and paste it into a *Notepad*, for later use.</span></span>

    ![](images/AzureLabs-Lab302b-16.png)

14. <span data-ttu-id="73331-208">Copiez également votre **ID de projet**, puis collez-le dans votre fichier *bloc-notes* pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="73331-208">Also copy your **Project Id**, and also paste it into your *Notepad* file, for later use.</span></span>

    ![](images/AzureLabs-Lab302b-16a.png)

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="73331-209">Chapitre 3-configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="73331-209">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="73331-210">Ce qui suit est une configuration classique pour le développement avec une réalité mixte, et, par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="73331-210">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="73331-211">Ouvrez *Unity* et cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="73331-211">Open *Unity* and click **New**.</span></span>

    ![](images/AzureLabs-Lab302b-17.png)

2.  <span data-ttu-id="73331-212">Vous devez maintenant fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-212">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="73331-213">Insérez **AzureCustomVision.**</span><span class="sxs-lookup"><span data-stu-id="73331-213">Insert **AzureCustomVision.**</span></span> <span data-ttu-id="73331-214">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="73331-214">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="73331-215">Définissez l' **emplacement** approprié pour vous (n’oubliez pas que les répertoires racine sont mieux adaptés).</span><span class="sxs-lookup"><span data-stu-id="73331-215">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="73331-216">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="73331-216">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab302b-18.png)

3.  <span data-ttu-id="73331-217">Si Unity est ouvert, il est conseillé de vérifier que l' **éditeur de script** par défaut est défini sur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-217">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="73331-218">Accédez à **modifier* > les*Préférences\*\* , puis à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="73331-218">Go to **Edit* > *Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="73331-219">Remplacez l' **éditeur de script externe** par **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="73331-219">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="73331-220">Fermez la fenêtre **Préférences** .</span><span class="sxs-lookup"><span data-stu-id="73331-220">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab302b-19.png)

4.  <span data-ttu-id="73331-221">Accédez ensuite à **fichier > paramètres de build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le bouton **changer de plateforme** pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="73331-221">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![](images/AzureLabs-Lab302b-20.png)

5.  <span data-ttu-id="73331-222">Tout en conservant les **paramètres de génération de > de fichiers** et assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="73331-222">While still in **File > Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="73331-223">L' **appareil cible** est défini sur **Hololens**</span><span class="sxs-lookup"><span data-stu-id="73331-223">**Target Device** is set to **Hololens**</span></span>

        > <span data-ttu-id="73331-224">Pour les casques immersifs, définissez **appareil cible** sur *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="73331-224">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>
        
    2.  <span data-ttu-id="73331-225">Le **type de build** est **D3D**</span><span class="sxs-lookup"><span data-stu-id="73331-225">**Build Type** is set to **D3D**</span></span>
    3.  <span data-ttu-id="73331-226">Le **SDK** est configuré sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="73331-226">**SDK** is set to **Latest installed**</span></span>
    4.  <span data-ttu-id="73331-227">**Version de Visual Studio** définie sur le **dernier installé**</span><span class="sxs-lookup"><span data-stu-id="73331-227">**Visual Studio Version** is set to **Latest installed**</span></span>
    5.  <span data-ttu-id="73331-228">La **génération et l’exécution** sont définies sur l' **ordinateur local**</span><span class="sxs-lookup"><span data-stu-id="73331-228">**Build and Run** is set to **Local Machine**</span></span>
    6.  <span data-ttu-id="73331-229">Enregistrez la scène et ajoutez-la à la Build.</span><span class="sxs-lookup"><span data-stu-id="73331-229">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="73331-230">Pour ce faire, sélectionnez **Ajouter des scènes ouvertes**.</span><span class="sxs-lookup"><span data-stu-id="73331-230">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="73331-231">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="73331-231">A save window will appear.</span></span>

            ![](images/AzureLabs-Lab302b-21.png)

        2. <span data-ttu-id="73331-232">Créez un dossier pour cela, ainsi que toute nouvelle scène, puis sélectionnez le bouton **nouveau dossier** pour créer un nouveau dossier, puis nommez- le Scenes.</span><span class="sxs-lookup"><span data-stu-id="73331-232">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![](images/AzureLabs-Lab302b-22.png)

        3. <span data-ttu-id="73331-233">Ouvrez le dossier scenes nouvellement créé, puis dans le champ *nom de fichier:* , tapez **CustomVisionScene**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="73331-233">Open your newly created **Scenes** folder, and then in the *File name:* text field, type **CustomVisionScene**, then click on **Save**.</span></span>

            ![](images/AzureLabs-Lab302b-23.png)

            > <span data-ttu-id="73331-234">Sachez que vous devez enregistrer vos scènes Unity dans le dossier *ressources* , car elles doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-234">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity project.</span></span> <span data-ttu-id="73331-235">La création du dossier scenes (et d’autres dossiers similaires) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-235">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>
            
    7.  <span data-ttu-id="73331-236">Les paramètres restants, dans *paramètres de build*, doivent être laissés par défaut pour le moment.</span><span class="sxs-lookup"><span data-stu-id="73331-236">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

        ![](images/AzureLabs-Lab302b-24.png)

6.  <span data-ttu-id="73331-237">Dans la fenêtre *paramètres de build* , cliquez sur le bouton Paramètres du **lecteur** pour ouvrir le panneau correspondant dans l’espace où se trouve l' *inspecteur* .</span><span class="sxs-lookup"><span data-stu-id="73331-237">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span>

7. <span data-ttu-id="73331-238">Dans ce volet, quelques paramètres doivent être vérifiés:</span><span class="sxs-lookup"><span data-stu-id="73331-238">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="73331-239">Sous l’onglet **autres paramètres** :</span><span class="sxs-lookup"><span data-stu-id="73331-239">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="73331-240">La **version du runtime de script** doit être **expérimentale (.net 4,6 équivalent)** , ce qui déclenche la nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="73331-240">**Scripting Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**, which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="73331-241">Le **backend de script** doit être **.net**</span><span class="sxs-lookup"><span data-stu-id="73331-241">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="73331-242">Le **niveau de compatibilité** de l’API doit être **.net 4,6**</span><span class="sxs-lookup"><span data-stu-id="73331-242">**API Compatibility Level** should be **.NET 4.6**</span></span>

        ![](images/AzureLabs-Lab302b-25.png)

    2.  <span data-ttu-id="73331-243">Dans l’onglet **paramètres de publication** , sous **fonctionnalités**, activez la case à cocher:</span><span class="sxs-lookup"><span data-stu-id="73331-243">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="73331-244">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="73331-244">**InternetClient**</span></span>

        2.  <span data-ttu-id="73331-245">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="73331-245">**Webcam**</span></span>

        3. <span data-ttu-id="73331-246">**Cravate**</span><span class="sxs-lookup"><span data-stu-id="73331-246">**Microphone**</span></span>

        ![](images/AzureLabs-Lab302b-26.png)

    3.  <span data-ttu-id="73331-247">Plus bas dans le volet, dans les **paramètres XR** (situés sous **paramètres de publication**), cochez la **réalité virtuelle prise en charge**, assurez-vous que le **Kit de développement logiciel (SDK) Windows Mixed Reality** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="73331-247">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

    ![](images/AzureLabs-Lab302b-27.png)

8.  <span data-ttu-id="73331-248">De retour dans les *paramètres de build* les *\# projets Unit C* ne sont plus grisés; cochez la case en regard de cette option.</span><span class="sxs-lookup"><span data-stu-id="73331-248">Back in *Build Settings* *Unity C\# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="73331-249">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="73331-249">Close the Build Settings window.</span></span>

10.  <span data-ttu-id="73331-250">Enregistrez votre scène et votre projet (**fichier > enregistrer la scène/le fichier > enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="73331-250">Save your Scene and project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>


## <a name="chapter-4---importing-the-newtonsoft-dll-in-unity"></a><span data-ttu-id="73331-251">Chapitre 4-importation de la DLL Newtonsoft dans Unity</span><span class="sxs-lookup"><span data-stu-id="73331-251">Chapter 4 - Importing the Newtonsoft DLL in Unity</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73331-252">Si vous souhaitez ignorer le composant *Unity Set up* de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce fichier [Azure-Mr-302b. pour Unity](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), à l’importer dans votre projet en tant que [**package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis à passer au [chapitre 6 ](#chapter-6---create-the-customvisionanalyser-class).</span><span class="sxs-lookup"><span data-stu-id="73331-252">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-302b.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 6](#chapter-6---create-the-customvisionanalyser-class).</span></span>

<span data-ttu-id="73331-253">Ce cours requiert l’utilisation de la bibliothèque **Newtonsoft** , que vous pouvez ajouter en tant que dll à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="73331-253">This course requires the use of the **Newtonsoft** library, which you can add as a DLL to your assets.</span></span> <span data-ttu-id="73331-254">Le package contenant [cette bibliothèque peut être téléchargé à partir de ce lien](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="73331-254">The package containing [this library can be downloaded from this Link](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).</span></span>
<span data-ttu-id="73331-255">Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le package Unity fourni avec ce cours.</span><span class="sxs-lookup"><span data-stu-id="73331-255">To import the Newtonsoft library into your project, use the Unity Package which came with this course.</span></span>

1.  <span data-ttu-id="73331-256">Ajoutez le fichier *. pour Unity* à Unity à l’aide de l’option de menu  **package* *personnalisé* du *package* > d'*importation\* de *ressources* > \* .</span><span class="sxs-lookup"><span data-stu-id="73331-256">Add the *.unitypackage* to Unity by using the **Assets* > *Import* *Package* > *Custom* *Package** menu option.</span></span>

2.  <span data-ttu-id="73331-257">Dans la zone **importer le package Unity** qui s’affiche, vérifiez que tous les plug- **ins** sous (et y compris) sont sélectionnés.</span><span class="sxs-lookup"><span data-stu-id="73331-257">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![](images/AzureLabs-Lab302b-28.png)

3.  <span data-ttu-id="73331-258">Cliquez sur le bouton **Importer** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="73331-258">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="73331-259">Accédez au dossier **Newtonsoft** sous **plug-ins** dans la vue projet et sélectionnez le *plug-in Newtonsoft. JSON*.</span><span class="sxs-lookup"><span data-stu-id="73331-259">Go to the **Newtonsoft** folder under **Plugins** in the project view and select the *Newtonsoft.Json plugin*.</span></span>

    ![](images/AzureLabs-Lab302b-29.png)

5.  <span data-ttu-id="73331-260">Une fois le *plug-in Newtonsoft. JSON* sélectionné, assurez-vous que **toutes les plateformes** sont décochées, vérifiez que **WSAPlayer** est également **désactivé**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="73331-260">With the *Newtonsoft.Json plugin* selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="73331-261">Cela vous permet de vérifier que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="73331-261">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab302b-30.png)

    > [!NOTE]
    > <span data-ttu-id="73331-262">Le marquage de ces plug-ins permet de les configurer pour qu’ils soient utilisés uniquement dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-262">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="73331-263">Il y en a un ensemble différent dans le dossier WSA qui sera utilisé une fois que le projet est exporté d’Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-263">There are a different set of them in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="73331-264">Ensuite, vous devez ouvrir le dossier **WSA** , dans le dossier **Newtonsoft** .</span><span class="sxs-lookup"><span data-stu-id="73331-264">Next, you need to open the **WSA** folder, within the **Newtonsoft** folder.</span></span> <span data-ttu-id="73331-265">Vous verrez une copie du même fichier que celui que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="73331-265">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="73331-266">Sélectionnez le fichier, puis, dans l’inspecteur, vérifiez que</span><span class="sxs-lookup"><span data-stu-id="73331-266">Select the file, and then in the inspector, ensure that</span></span>
    -   <span data-ttu-id="73331-267">**Aucune plateforme** n'  est désactivée</span><span class="sxs-lookup"><span data-stu-id="73331-267">**Any Platform** is **unchecked**</span></span> 
    -   <span data-ttu-id="73331-268">**uniquement** **WSAPlayer** est **activé**</span><span class="sxs-lookup"><span data-stu-id="73331-268">**only** **WSAPlayer** is **checked**</span></span>
    -   <span data-ttu-id="73331-269">L’option ne pas **traiter le processus** est **activée**</span><span class="sxs-lookup"><span data-stu-id="73331-269">**Dont process** is **checked**</span></span>

    ![](images/AzureLabs-Lab302b-31.png)

## <a name="chapter-5---camera-setup"></a><span data-ttu-id="73331-270">Chapitre 5-Configuration de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="73331-270">Chapter 5 - Camera setup</span></span>

1.  <span data-ttu-id="73331-271">Dans le panneau hiérarchie, sélectionnez l' *appareil photo principal*.</span><span class="sxs-lookup"><span data-stu-id="73331-271">In the Hierarchy Panel, select the *Main Camera*.</span></span>

2.  <span data-ttu-id="73331-272">Une fois sélectionné, vous pouvez voir tous les composants de la *caméra principale* dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="73331-272">Once selected, you will be able to see all the components of the *Main Camera* in the *Inspector Panel*.</span></span>

    1.  <span data-ttu-id="73331-273">L’objet *Camera* doit être nommé **Camera main** (Notez l’orthographe!)</span><span class="sxs-lookup"><span data-stu-id="73331-273">The *camera* object must be named **Main Camera** (note the spelling!)</span></span>

    2.  <span data-ttu-id="73331-274">La balise  principale de l’appareil photo doit être définie sur **MainCamera** (Notez l’orthographe!)</span><span class="sxs-lookup"><span data-stu-id="73331-274">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3.  <span data-ttu-id="73331-275">Vérifiez que la **position** de la transformation est définie sur **0, 0,** 0</span><span class="sxs-lookup"><span data-stu-id="73331-275">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4.  <span data-ttu-id="73331-276">Affectez à **effacer les indicateurs** la **couleur unie** (ignorer ce point pour le casque immersif).</span><span class="sxs-lookup"><span data-stu-id="73331-276">Set **Clear Flags** to **Solid Color** (ignore this for immersive headset).</span></span>

    5.  <span data-ttu-id="73331-277">Définissez la couleur d' **arrière-plan** du composant Camera sur **Black, alpha 0 (Code hex: #00000000)** (ignorez-le pour le casque immersif).</span><span class="sxs-lookup"><span data-stu-id="73331-277">Set the **Background** Color of the camera Component to **Black, Alpha 0 (Hex Code: #00000000)** (ignore this for immersive headset).</span></span>

    ![](images/AzureLabs-Lab302b-32.png)


## <a name="chapter-6---create-the-customvisionanalyser-class"></a><span data-ttu-id="73331-278">Chapitre 6-créer la classe CustomVisionAnalyser.</span><span class="sxs-lookup"><span data-stu-id="73331-278">Chapter 6 - Create the CustomVisionAnalyser class.</span></span>

<span data-ttu-id="73331-279">À ce stade, vous êtes prêt à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="73331-279">At this point you are ready to write some code.</span></span>

<span data-ttu-id="73331-280">Vous allez commencer par la classe *CustomVisionAnalyser* .</span><span class="sxs-lookup"><span data-stu-id="73331-280">You will begin with the *CustomVisionAnalyser* class.</span></span>

> [!NOTE]
> <span data-ttu-id="73331-281">Les appels au **service vision personnalisée** effectués dans le code ci-dessous sont effectués à l’aide de l' **API REST Custom vision**.</span><span class="sxs-lookup"><span data-stu-id="73331-281">The calls to the **Custom Vision Service** made in the code shown below are made using the **Custom Vision REST API**.</span></span> <span data-ttu-id="73331-282">À l’aide de ce guide, vous allez apprendre à implémenter et à utiliser cette API (utile pour comprendre comment implémenter des éléments similaires).</span><span class="sxs-lookup"><span data-stu-id="73331-282">Through using this, you will see how to implement and make use of this API (useful for understanding how to implement something similar on your own).</span></span> <span data-ttu-id="73331-283">Sachez que Microsoft propose un **Kit de développement logiciel (SDK) service vision personnalisée** qui peut également être utilisé pour effectuer des appels au service.</span><span class="sxs-lookup"><span data-stu-id="73331-283">Be aware, that Microsoft offers a **Custom Vision Service SDK** that can also be used to make calls to the Service.</span></span> <span data-ttu-id="73331-284">Pour plus d’informations, consultez l’article du [Kit de développement logiciel (SDK) service vision personnalisée](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) .</span><span class="sxs-lookup"><span data-stu-id="73331-284">For more information visit the [Custom Vision Service SDK](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) article.</span></span>

<span data-ttu-id="73331-285">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="73331-285">This class is responsible for:</span></span>

-   <span data-ttu-id="73331-286">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="73331-286">Loading the latest image captured as an array of bytes.</span></span>

-   <span data-ttu-id="73331-287">Envoi du tableau d’octets à votre instance Azure *service vision personnalisée* à des fins d’analyse.</span><span class="sxs-lookup"><span data-stu-id="73331-287">Sending the byte array to your Azure *Custom Vision Service* instance for analysis.</span></span>

-   <span data-ttu-id="73331-288">Réception de la réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="73331-288">Receiving the response as a JSON string.</span></span>

-   <span data-ttu-id="73331-289">La désérialisation de la réponse et le passage  de la prédiction résultante à la classe *SceneOrganiser* , qui s’occupera du mode d’affichage de la réponse.</span><span class="sxs-lookup"><span data-stu-id="73331-289">Deserializing the response and passing the resulting *Prediction* to the *SceneOrganiser* class, which will take care of how the response should be displayed.</span></span>

<span data-ttu-id="73331-290">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-290">To create this class:</span></span>

1.  <span data-ttu-id="73331-291">Cliquez avec le bouton droit sur le *dossier Asset* situé dans le *panneau Projet*, puis cliquez sur **créer un dossier >** .</span><span class="sxs-lookup"><span data-stu-id="73331-291">Right-click in the *Asset Folder* located in the *Project Panel*, then click **Create > Folder**.</span></span> <span data-ttu-id="73331-292">Appelez le dossier **scripts**.</span><span class="sxs-lookup"><span data-stu-id="73331-292">Call the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab302b-33.png)

2.  <span data-ttu-id="73331-293">Double-cliquez sur le dossier que vous venez de créer pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="73331-293">Double-click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="73331-294">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-294">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="73331-295">Nommez le script *CustomVisionAnalyser*.</span><span class="sxs-lookup"><span data-stu-id="73331-295">Name the script *CustomVisionAnalyser*.</span></span>

4.  <span data-ttu-id="73331-296">Double-cliquez sur le nouveau script *CustomVisionAnalyser* pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-296">Double-click on the new *CustomVisionAnalyser* script to open it with **Visual Studio**.</span></span>

5.  <span data-ttu-id="73331-297">Mettez à jour les espaces de noms en haut de votre fichier pour qu’ils correspondent à ce qui suit:</span><span class="sxs-lookup"><span data-stu-id="73331-297">Update the namespaces at the top of your file to match the following:</span></span>

    ```csharp
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    using Newtonsoft.Json;
    ```

6.  <span data-ttu-id="73331-298">Dans la classe *CustomVisionAnalyser* , ajoutez les variables suivantes:</span><span class="sxs-lookup"><span data-stu-id="73331-298">In the *CustomVisionAnalyser* class, add the following variables:</span></span>

    ```csharp
        /// <summary>
        /// Unique instance of this class
        /// </summary>
        public static CustomVisionAnalyser Instance;

        /// <summary>
        /// Insert your Prediction Key here
        /// </summary>
        private string predictionKey = "- Insert your key here -";

        /// <summary>
        /// Insert your prediction endpoint here
        /// </summary>
        private string predictionEndpoint = "Insert your prediction endpoint here";

        /// <summary>
        /// Byte array of the image to submit for analysis
        /// </summary>
        [HideInInspector] public byte[] imageBytes;
    ```

    > [!NOTE]
    > <span data-ttu-id="73331-299">Veillez à insérer votre **clé** de prédiction dans la variable **PredictionKey** et votre **point de terminaison** de prédiction dans la variable **predictionEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="73331-299">Make sure you insert your **Prediction Key** into the **predictionKey** variable and your **Prediction Endpoint** into the **predictionEndpoint** variable.</span></span> <span data-ttu-id="73331-300">Vous les avez copiées dans le *bloc-notes* plus tôt dans le cours.</span><span class="sxs-lookup"><span data-stu-id="73331-300">You copied these to *Notepad* earlier in the course.</span></span>

7.  <span data-ttu-id="73331-301">Le code pour **éveillé ()** doit maintenant être ajouté pour initialiser la variable d’instance:</span><span class="sxs-lookup"><span data-stu-id="73331-301">Code for **Awake()** now needs to be added to initialize the Instance variable:</span></span>

    ```csharp
        /// <summary>
        /// Initialises this class
        /// </summary>
        private void Awake()
        {
            // Allows this instance to behave like a singleton
            Instance = this;
        }
    ```

8.  <span data-ttu-id="73331-302">Supprimez les méthodes **Start ()** et **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-302">Delete the methods **Start()** and **Update()**.</span></span>

9.  <span data-ttu-id="73331-303">Ensuite, ajoutez la Coroutine (avec la méthode statique **GetImageAsByteArray ()** en dessous de celle-ci), qui obtiendra les résultats de l’analyse de l’image capturée par la classe *ImageCapture* .</span><span class="sxs-lookup"><span data-stu-id="73331-303">Next, add the coroutine (with the static **GetImageAsByteArray()** method below it), which will obtain the results of the analysis of the image captured by the *ImageCapture* class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="73331-304">Dans la Coroutine **AnalyseImageCapture** , il y a un appel à la classe *SceneOrganiser* que vous êtes encore en cours de création.</span><span class="sxs-lookup"><span data-stu-id="73331-304">In the **AnalyseImageCapture** coroutine, there is a call to the *SceneOrganiser* class that you are yet to create.</span></span> <span data-ttu-id="73331-305">Par conséquent, **laissez ces lignes commentées pour l’instant**.</span><span class="sxs-lookup"><span data-stu-id="73331-305">Therefore, **leave those lines commented for now**.</span></span>

    ```csharp    
        /// <summary>
        /// Call the Computer Vision Service to submit the image.
        /// </summary>
        public IEnumerator AnalyseLastImageCaptured(string imagePath)
        {
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

                // The response will be in JSON format, therefore it needs to be deserialized    
    
                // The following lines refers to a class that you will build in later Chapters
                // Wait until then to uncomment these lines

                //AnalysisObject analysisObject = new AnalysisObject();
                //analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
                //SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
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

10.  <span data-ttu-id="73331-306">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-306">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

## <a name="chapter-7---create-the-customvisionobjects-class"></a><span data-ttu-id="73331-307">Chapitre 7-créer la classe CustomVisionObjects</span><span class="sxs-lookup"><span data-stu-id="73331-307">Chapter 7 - Create the CustomVisionObjects class</span></span>

<span data-ttu-id="73331-308">La classe que vous allez créer est maintenant la classe *CustomVisionObjects* .</span><span class="sxs-lookup"><span data-stu-id="73331-308">The class you will create now is the *CustomVisionObjects* class.</span></span>

<span data-ttu-id="73331-309">Ce script contient un certain nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels passés au *service vision personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="73331-309">This script contains a number of objects used by other classes to serialize and deserialize the calls made to the *Custom Vision Service*.</span></span>

> [!WARNING]
> <span data-ttu-id="73331-310">Il est important de noter le point de terminaison que la Service Vision personnalisée vous fournit, car la structure JSON ci-dessous a été configurée pour fonctionner avec [*Custom vision prédiction v 2.0*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290).</span><span class="sxs-lookup"><span data-stu-id="73331-310">It is important that you take note of the endpoint that the Custom Vision Service provides you, as the below JSON structure has been set up to work with [*Custom Vision Prediction v2.0*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290).</span></span> <span data-ttu-id="73331-311">Si vous disposez d’une version différente, vous devrez peut-être mettre à jour la structure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="73331-311">If you have a different version, you may need to update the below structure.</span></span>

<span data-ttu-id="73331-312">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-312">To create this class:</span></span>

1.  <span data-ttu-id="73331-313">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-313">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="73331-314">Appelez le script *CustomVisionObjects*.</span><span class="sxs-lookup"><span data-stu-id="73331-314">Call the script *CustomVisionObjects*.</span></span>

2.  <span data-ttu-id="73331-315">Double-cliquez sur le nouveau script **CustomVisionObjects** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-315">Double-click on the new **CustomVisionObjects** script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="73331-316">Ajoutez les espaces de noms suivants au début du fichier:</span><span class="sxs-lookup"><span data-stu-id="73331-316">Add the following namespaces to the top of the file:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="73331-317">Supprimez les méthodes **Start ()** et **Update ()** à l’intérieur de la classe *CustomVisionObjects* ; Cette classe doit maintenant être vide.</span><span class="sxs-lookup"><span data-stu-id="73331-317">Delete the **Start()** and **Update()** methods inside the *CustomVisionObjects* class; this class should now be empty.</span></span>

5.  <span data-ttu-id="73331-318">Ajoutez les classes suivantes **en dehors** de la classe *CustomVisionObjects* .</span><span class="sxs-lookup"><span data-stu-id="73331-318">Add the following classes **outside** the *CustomVisionObjects* class.</span></span> <span data-ttu-id="73331-319">Ces objets sont utilisés par la bibliothèque *Newtonsoft* pour sérialiser et désérialiser les données de réponse:</span><span class="sxs-lookup"><span data-stu-id="73331-319">These objects are used by the *Newtonsoft* library to serialize and deserialize the response data:</span></span>

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
    /// JSON of Images submitted
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
    /// Predictions received by the Service after submitting an image for analysis
    /// </summary> 
    [Serializable]
    public class AnalysisObject
    {
        public List<Prediction> Predictions { get; set; }
    }

    [Serializable]
    public class Prediction
    {
        public string TagName { get; set; }
        public double Probability { get; set; }
    }
    ```

## <a name="chapter-8---create-the-voicerecognizer-class"></a><span data-ttu-id="73331-320">Chapitre 8-créer la classe VoiceRecognizer</span><span class="sxs-lookup"><span data-stu-id="73331-320">Chapter 8 - Create the VoiceRecognizer class</span></span>

<span data-ttu-id="73331-321">Cette classe reconnaît la saisie vocale de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73331-321">This class will recognize the voice input from the user.</span></span>

<span data-ttu-id="73331-322">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-322">To create this class:</span></span>

1.  <span data-ttu-id="73331-323">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-323">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="73331-324">Appelez le script *VoiceRecognizer*.</span><span class="sxs-lookup"><span data-stu-id="73331-324">Call the script *VoiceRecognizer*.</span></span>

2.  <span data-ttu-id="73331-325">Double-cliquez sur le nouveau script **VoiceRecognizer** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-325">Double-click on the new **VoiceRecognizer** script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="73331-326">Ajoutez les espaces de noms suivants au-dessus de la classe *VoiceRecognizer* :</span><span class="sxs-lookup"><span data-stu-id="73331-326">Add the following namespaces above the *VoiceRecognizer* class:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.Windows.Speech;
    ```

4.  <span data-ttu-id="73331-327">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *VoiceRecognizer* , au-dessus de la méthode *Start ()* :</span><span class="sxs-lookup"><span data-stu-id="73331-327">Then add the following variables inside the *VoiceRecognizer* class, above the *Start()* method:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static VoiceRecognizer Instance;

        /// <summary>
        /// Recognizer class for voice recognition
        /// </summary>
        internal KeywordRecognizer keywordRecognizer;

        /// <summary>
        /// List of Keywords registered
        /// </summary>
        private Dictionary<string, Action> _keywords = new Dictionary<string, Action>();
    ```

5.  <span data-ttu-id="73331-328">Ajoutez les méthodes **éveillé ()** et **Start ()** , dont la dernière configurera les *Mots clés* utilisateur pour qu’ils soient reconnus lors de l’Association d’une balise à une image:</span><span class="sxs-lookup"><span data-stu-id="73331-328">Add the **Awake()** and **Start()** methods, the latter of which will set up the user *keywords* to be recognized when associating a tag to an image:</span></span>

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
        void Start ()
        {

            Array tagsArray = Enum.GetValues(typeof(CustomVisionTrainer.Tags));

            foreach (object tagWord in tagsArray)
            {
                _keywords.Add(tagWord.ToString(), () =>
                {
                    // When a word is recognized, the following line will be called
                    CustomVisionTrainer.Instance.VerifyTag(tagWord.ToString());
                });
            }

            _keywords.Add("Discard", () =>
            {
                // When a word is recognized, the following line will be called
                // The user does not want to submit the image
                // therefore ignore and discard the process
                ImageCapture.Instance.ResetImageCapture();
                keywordRecognizer.Stop();
            });

            //Create the keyword recognizer 
            keywordRecognizer = new KeywordRecognizer(_keywords.Keys.ToArray());

            // Register for the OnPhraseRecognized event 
            keywordRecognizer.OnPhraseRecognized += KeywordRecognizer_OnPhraseRecognized;
        }
    ```

6.  <span data-ttu-id="73331-329">Supprimez la méthode **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-329">Delete the **Update()** method.</span></span>

7.  <span data-ttu-id="73331-330">Ajoutez le gestionnaire suivant, qui est appelé chaque fois que l’entrée vocale est reconnue:</span><span class="sxs-lookup"><span data-stu-id="73331-330">Add the following handler, which is called whenever voice input is recognized:</span></span>

    ```csharp    
        /// <summary>
        /// Handler called when a word is recognized
        /// </summary>
        private void KeywordRecognizer_OnPhraseRecognized(PhraseRecognizedEventArgs args)
        {
            Action keywordAction;
            // if the keyword recognized is in our dictionary, call that Action.
            if (_keywords.TryGetValue(args.text, out keywordAction))
            {
                keywordAction.Invoke();
            }
        }
    ```

8.  <span data-ttu-id="73331-331">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-331">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

> [!NOTE]
> <span data-ttu-id="73331-332">Ne vous inquiétez pas du code qui peut sembler avoir une erreur, car vous fournirez bientôt d’autres classes, ce qui les corrigera.</span><span class="sxs-lookup"><span data-stu-id="73331-332">Do not worry about code which might appear to have an error, as you will provide further classes soon, which will fix these.</span></span>

## <a name="chapter-9---create-the-customvisiontrainer-class"></a><span data-ttu-id="73331-333">Chapitre 9-créer la classe CustomVisionTrainer</span><span class="sxs-lookup"><span data-stu-id="73331-333">Chapter 9 - Create the CustomVisionTrainer class</span></span>

<span data-ttu-id="73331-334">Cette classe chaînera une série d’appels Web pour former l' *service vision personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="73331-334">This class will chain a series of web calls to train the *Custom Vision Service*.</span></span> <span data-ttu-id="73331-335">Chaque appel sera expliqué en détail juste au-dessus du code.</span><span class="sxs-lookup"><span data-stu-id="73331-335">Each call will be explained in detail right above the code.</span></span>

<span data-ttu-id="73331-336">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-336">To create this class:</span></span>

1.  <span data-ttu-id="73331-337">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-337">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="73331-338">Appelez le script *CustomVisionTrainer*.</span><span class="sxs-lookup"><span data-stu-id="73331-338">Call the script *CustomVisionTrainer*.</span></span>

2.  <span data-ttu-id="73331-339">Double-cliquez sur le nouveau script *CustomVisionTrainer* pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-339">Double-click on the new *CustomVisionTrainer* script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="73331-340">Ajoutez les espaces de noms suivants au-dessus de la classe *CustomVisionTrainer* :</span><span class="sxs-lookup"><span data-stu-id="73331-340">Add the following namespaces above the *CustomVisionTrainer* class:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="73331-341">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *CustomVisionTrainer* , au-dessus de la méthode **Start ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-341">Then add the following variables inside the *CustomVisionTrainer* class, above the **Start()** method.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="73331-342">L’URL de formation utilisée ici est fournie dans la documentation *Custom vision formation 1,2* et présente la structure suivante: https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/</span><span class="sxs-lookup"><span data-stu-id="73331-342">The training URL used here is provided within the *Custom Vision Training 1.2* documentation, and has a structure of: https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/</span></span>  
    > <span data-ttu-id="73331-343">Pour plus d’informations, consultez l' [*API de référence de Custom vision formation v 1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span><span class="sxs-lookup"><span data-stu-id="73331-343">For more information, visit the [*Custom Vision Training v1.2 reference API*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span></span>

    > [!WARNING]
    > <span data-ttu-id="73331-344">Il est important de noter le point de terminaison que la Service Vision personnalisée vous fournit pour le mode d’apprentissage, car la structure JSON utilisée (dans la classe **CustomVisionObjects** ) a été configurée pour fonctionner avec [*Custom vision formation v 1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span><span class="sxs-lookup"><span data-stu-id="73331-344">It is important that you take note of the endpoint that the Custom Vision Service provides you for the training mode, as the JSON structure used (within the **CustomVisionObjects** class) has been set up to work with [*Custom Vision Training v1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span></span> <span data-ttu-id="73331-345">Si vous disposez d’une version différente, vous devrez peut-être mettre à jour la structure des *objets* .</span><span class="sxs-lookup"><span data-stu-id="73331-345">If you have a different version, you may need to update the *Objects* structure.</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static CustomVisionTrainer Instance;

        /// <summary>
        /// Custom Vision Service URL root
        /// </summary>
        private string url = "https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/";

        /// <summary>
        /// Insert your prediction key here
        /// </summary>
        private string trainingKey = "- Insert your key here -";

        /// <summary>
        /// Insert your Project Id here
        /// </summary>
        private string projectId = "- Insert your Project Id here -";

        /// <summary>
        /// Byte array of the image to submit for analysis
        /// </summary>
        internal byte[] imageBytes;

        /// <summary>
        /// The Tags accepted
        /// </summary>
        internal enum Tags {Mouse, Keyboard}

        /// <summary>
        /// The UI displaying the training Chapters
        /// </summary>
        private TextMesh trainingUI_TextMesh;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="73331-346">Veillez à ajouter la valeur de **clé de service** (clé de formation) et la valeur d' **ID de projet** , que vous avez notée précédemment; Il s’agit des valeurs que vous avez [collectées à partir du portail plus haut dans le cours (chapitre 2, étape 10)](#chapter-2---training-your-custom-vision-oroject).</span><span class="sxs-lookup"><span data-stu-id="73331-346">Ensure that you add your **Service Key** (Training Key) value and **Project Id** value, which you noted down previous; these are the values you [collected from the portal earlier in the course (Chapter 2, step 10 onwards)](#chapter-2---training-your-custom-vision-oroject).</span></span>

5.  <span data-ttu-id="73331-347">Ajoutez les méthodes **Start ()** et **éveillé ()** suivantes.</span><span class="sxs-lookup"><span data-stu-id="73331-347">Add the following **Start()** and **Awake()** methods.</span></span> <span data-ttu-id="73331-348">Ces méthodes sont appelées lors de l’initialisation et contiennent l’appel pour configurer l’interface utilisateur:</span><span class="sxs-lookup"><span data-stu-id="73331-348">Those methods are called on initialization and contain the call to set up the UI:</span></span>

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
        private void Start()
        { 
            trainingUI_TextMesh = SceneOrganiser.Instance.CreateTrainingUI("TrainingUI", 0.04f, 0, 4, false);
        }
    ```

6.  <span data-ttu-id="73331-349">Supprimez la méthode **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-349">Delete the **Update()** method.</span></span> <span data-ttu-id="73331-350">Cette classe n’en a pas besoin.</span><span class="sxs-lookup"><span data-stu-id="73331-350">This class will not need it.</span></span>

7.  <span data-ttu-id="73331-351">Ajoutez la méthode **RequestTagSelection ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-351">Add the **RequestTagSelection()** method.</span></span> <span data-ttu-id="73331-352">Cette méthode est la première à être appelée lorsqu’une image a été capturée et stockée dans l’appareil et qu’elle est maintenant prête à être envoyée à la *service vision personnalisée*pour l’effectuer.</span><span class="sxs-lookup"><span data-stu-id="73331-352">This method is the first to be called when an image has been captured and stored in the device and is now ready to be submitted to the *Custom Vision Service*, to train it.</span></span> <span data-ttu-id="73331-353">Cette méthode affiche, dans l’interface utilisateur de formation, un ensemble de mots clés que l’utilisateur peut utiliser pour baliser l’image capturée.</span><span class="sxs-lookup"><span data-stu-id="73331-353">This method displays, in the training UI, a set of keywords the user can use to tag the image that has been captured.</span></span> <span data-ttu-id="73331-354">Elle alerte également la classe *VoiceRecognizer* pour commencer à écouter l’utilisateur pour l’entrée vocale.</span><span class="sxs-lookup"><span data-stu-id="73331-354">It also alerts the *VoiceRecognizer* class to begin listening to the user for voice input.</span></span>

    ```csharp
        internal void RequestTagSelection()
        {
            trainingUI_TextMesh.gameObject.SetActive(true);
            trainingUI_TextMesh.text = $" \nUse voice command \nto choose between the following tags: \nMouse\nKeyboard \nor say Discard";

            VoiceRecognizer.Instance.keywordRecognizer.Start();
        }
    ```

8.  <span data-ttu-id="73331-355">Ajoutez la méthode **VerifyTag ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-355">Add the **VerifyTag()** method.</span></span> <span data-ttu-id="73331-356">Cette méthode recevra l’entrée vocale reconnue par la classe **VoiceRecognizer** et vérifiera sa validité, puis commencera le processus d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="73331-356">This method will receive the voice input recognized by the **VoiceRecognizer** class and verify its validity, and then begin the training process.</span></span>

    ```csharp
        /// <summary>
        /// Verify voice input against stored tags.
        /// If positive, it will begin the Service training process.
        /// </summary>
        internal void VerifyTag(string spokenTag)
        {
            if (spokenTag == Tags.Mouse.ToString() || spokenTag == Tags.Keyboard.ToString())
            {
                trainingUI_TextMesh.text = $"Tag chosen: {spokenTag}";
                VoiceRecognizer.Instance.keywordRecognizer.Stop();
                StartCoroutine(SubmitImageForTraining(ImageCapture.Instance.filePath, spokenTag));
            }
        }
    ```

9.  <span data-ttu-id="73331-357">Ajoutez la méthode **SubmitImageForTraining ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-357">Add the **SubmitImageForTraining()** method.</span></span> <span data-ttu-id="73331-358">Cette méthode démarre le processus de formation Service Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="73331-358">This method will begin the Custom Vision Service training process.</span></span> <span data-ttu-id="73331-359">La première étape consiste à récupérer l' **ID** de balise à partir du service associé à l’entrée vocale validée de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73331-359">The first step is to retrieve the **Tag Id** from the Service which is associated with the validated speech input from the user.</span></span> <span data-ttu-id="73331-360">L' **ID** de balise sera ensuite téléchargé avec l’image.</span><span class="sxs-lookup"><span data-stu-id="73331-360">The **Tag Id** will then be uploaded along with the image.</span></span>

    ```csharp
        /// <summary>
        /// Call the Custom Vision Service to submit the image.
        /// </summary>
        public IEnumerator SubmitImageForTraining(string imagePath, string tag)
        {
            yield return new WaitForSeconds(2);
            trainingUI_TextMesh.text = $"Submitting Image \nwith tag: {tag} \nto Custom Vision Service";
            string imageId = string.Empty;
            string tagId = string.Empty;

            // Retrieving the Tag Id relative to the voice input
            string getTagIdEndpoint = string.Format("{0}{1}/tags", url, projectId);
            using (UnityWebRequest www = UnityWebRequest.Get(getTagIdEndpoint))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;

                Tags_RootObject tagRootObject = JsonConvert.DeserializeObject<Tags_RootObject>(jsonResponse);

                foreach (TagOfProject tOP in tagRootObject.Tags)
                {
                    if (tOP.Name == tag)
                    {
                        tagId = tOP.Id;
                    }             
                }
            }

            // Creating the image object to send for training
            List<IMultipartFormSection> multipartList = new List<IMultipartFormSection>();
            MultipartObject multipartObject = new MultipartObject();
            multipartObject.contentType = "application/octet-stream";
            multipartObject.fileName = "";
            multipartObject.sectionData = GetImageAsByteArray(imagePath);
            multipartList.Add(multipartObject);

            string createImageFromDataEndpoint = string.Format("{0}{1}/images?tagIds={2}", url, projectId, tagId);

            using (UnityWebRequest www = UnityWebRequest.Post(createImageFromDataEndpoint, multipartList))
            {
                // Gets a byte array out of the saved image
                imageBytes = GetImageAsByteArray(imagePath);           

                //unityWebRequest.SetRequestHeader("Content-Type", "application/octet-stream");
                www.SetRequestHeader("Training-Key", trainingKey);

                // The upload handler will help uploading the byte array with the request
                www.uploadHandler = new UploadHandlerRaw(imageBytes);

                // The download handler will help receiving the analysis from Azure
                www.downloadHandler = new DownloadHandlerBuffer();

                // Send the request
                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                ImageRootObject m = JsonConvert.DeserializeObject<ImageRootObject>(jsonResponse);
                imageId = m.Images[0].Image.Id;
            }
            trainingUI_TextMesh.text = "Image uploaded";
            StartCoroutine(TrainCustomVisionProject());
        }
    ```

10. <span data-ttu-id="73331-361">Ajoutez la méthode **TrainCustomVisionProject ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-361">Add the **TrainCustomVisionProject()** method.</span></span> <span data-ttu-id="73331-362">Une fois que l’image a été envoyée et balisée, cette méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="73331-362">Once the image has been submitted and tagged, this method will be called.</span></span> <span data-ttu-id="73331-363">Il créera une nouvelle itération qui sera formée avec toutes les images précédentes soumises au service, ainsi que l’image qui vient d’être téléchargée.</span><span class="sxs-lookup"><span data-stu-id="73331-363">It will create a new Iteration that will be trained with all the previous images submitted to the Service plus the image just uploaded.</span></span> <span data-ttu-id="73331-364">Une fois l’apprentissage terminé, cette méthode appellera une méthode pour définir l' **itération** nouvellement créée **par défaut**, afin que le point de terminaison que vous utilisez pour l’analyse soit la dernière itération formée.</span><span class="sxs-lookup"><span data-stu-id="73331-364">Once the training has been completed, this method will call a method to set the newly created **Iteration** as **Default**, so that the endpoint you are using for analysis is the latest trained iteration.</span></span>

    ```csharp
        /// <summary>
        /// Call the Custom Vision Service to train the Service.
        /// It will generate a new Iteration in the Service
        /// </summary>
        public IEnumerator TrainCustomVisionProject()
        {
            yield return new WaitForSeconds(2);

            trainingUI_TextMesh.text = "Training Custom Vision Service";

            WWWForm webForm = new WWWForm();

            string trainProjectEndpoint = string.Format("{0}{1}/train", url, projectId);

            using (UnityWebRequest www = UnityWebRequest.Post(trainProjectEndpoint, webForm))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();
                string jsonResponse = www.downloadHandler.text;
                Debug.Log($"Training - JSON Response: {jsonResponse}");

                // A new iteration that has just been created and trained
                Iteration iteration = new Iteration();
                iteration = JsonConvert.DeserializeObject<Iteration>(jsonResponse);

                if (www.isDone)
                {
                    trainingUI_TextMesh.text = "Custom Vision Trained";

                    // Since the Service has a limited number of iterations available,
                    // we need to set the last trained iteration as default
                    // and delete all the iterations you dont need anymore
                    StartCoroutine(SetDefaultIteration(iteration)); 
                }
            }
        }
    ```

11. <span data-ttu-id="73331-365">Ajoutez la méthode **SetDefaultIteration ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-365">Add the **SetDefaultIteration()** method.</span></span> <span data-ttu-id="73331-366">Cette méthode définit l’itération précédemment créée et formée comme *valeur par défaut*.</span><span class="sxs-lookup"><span data-stu-id="73331-366">This method will set the previously created and trained iteration as *Default*.</span></span> <span data-ttu-id="73331-367">Une fois l’opération terminée, cette méthode devra supprimer l’itération précédente existante dans le service.</span><span class="sxs-lookup"><span data-stu-id="73331-367">Once completed, this method will have to delete the previous iteration existing in the Service.</span></span> <span data-ttu-id="73331-368">Au moment de la rédaction de ce cours, il existe une limite de dix (10) itérations maximum autorisées à exister simultanément dans le service.</span><span class="sxs-lookup"><span data-stu-id="73331-368">At the time of writing this course, there is a limit of a maximum ten (10) iterations allowed to exist at the same time in the Service.</span></span>

    ```csharp
        /// <summary>
        /// Set the newly created iteration as Default
        /// </summary>
        private IEnumerator SetDefaultIteration(Iteration iteration)
        {
            yield return new WaitForSeconds(5);
            trainingUI_TextMesh.text = "Setting default iteration";

            // Set the last trained iteration to default
            iteration.IsDefault = true;

            // Convert the iteration object as JSON
            string iterationAsJson = JsonConvert.SerializeObject(iteration);
            byte[] bytes = Encoding.UTF8.GetBytes(iterationAsJson);

            string setDefaultIterationEndpoint = string.Format("{0}{1}/iterations/{2}", 
                                                            url, projectId, iteration.Id);

            using (UnityWebRequest www = UnityWebRequest.Put(setDefaultIterationEndpoint, bytes))
            {
                www.method = "PATCH";
                www.SetRequestHeader("Training-Key", trainingKey);
                www.SetRequestHeader("Content-Type", "application/json");
                www.downloadHandler = new DownloadHandlerBuffer();

                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                if (www.isDone)
                {
                    trainingUI_TextMesh.text = "Default iteration is set \nDeleting Unused Iteration";
                    StartCoroutine(DeletePreviousIteration(iteration));
                }
            }
        }
    ```

12. <span data-ttu-id="73331-369">Ajoutez la méthode **DeletePreviousIteration ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-369">Add the **DeletePreviousIteration()** method.</span></span> <span data-ttu-id="73331-370">Cette méthode recherche et supprime l’itération précédente non définie par défaut:</span><span class="sxs-lookup"><span data-stu-id="73331-370">This method will find and delete the previous non-default iteration:</span></span>

    ```csharp
        /// <summary>
        /// Delete the previous non-default iteration.
        /// </summary>
        public IEnumerator DeletePreviousIteration(Iteration iteration)
        {
            yield return new WaitForSeconds(5);

            trainingUI_TextMesh.text = "Deleting Unused \nIteration";

            string iterationToDeleteId = string.Empty;

            string findAllIterationsEndpoint = string.Format("{0}{1}/iterations", url, projectId);

            using (UnityWebRequest www = UnityWebRequest.Get(findAllIterationsEndpoint))
            {
                www.SetRequestHeader("Training-Key", trainingKey);
                www.downloadHandler = new DownloadHandlerBuffer();
                yield return www.SendWebRequest();

                string jsonResponse = www.downloadHandler.text;

                // The iteration that has just been trained
                List<Iteration> iterationsList = new List<Iteration>();
                iterationsList = JsonConvert.DeserializeObject<List<Iteration>>(jsonResponse);

                foreach (Iteration i in iterationsList)
                {
                    if (i.IsDefault != true)
                    {
                        Debug.Log($"Cleaning - Deleting iteration: {i.Name}, {i.Id}");
                        iterationToDeleteId = i.Id;
                        break;
                    }
                }
            }

            string deleteEndpoint = string.Format("{0}{1}/iterations/{2}", url, projectId, iterationToDeleteId);

            using (UnityWebRequest www2 = UnityWebRequest.Delete(deleteEndpoint))
            {
                www2.SetRequestHeader("Training-Key", trainingKey);
                www2.downloadHandler = new DownloadHandlerBuffer();
                yield return www2.SendWebRequest();
                string jsonResponse = www2.downloadHandler.text;

                trainingUI_TextMesh.text = "Iteration Deleted";
                yield return new WaitForSeconds(2);
                trainingUI_TextMesh.text = "Ready for next \ncapture";

                yield return new WaitForSeconds(2);
                trainingUI_TextMesh.text = "";
                ImageCapture.Instance.ResetImageCapture();
            }
        }
    ```

13. <span data-ttu-id="73331-371">La dernière méthode à ajouter dans cette classe est la méthode **GetImageAsByteArray ()** , utilisée sur les appels Web pour convertir l’image capturée dans un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="73331-371">The last method to add in this class is the **GetImageAsByteArray()** method, used on the web calls to convert the image captured into a byte array.</span></span>

    ```csharp
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

14. <span data-ttu-id="73331-372">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-372">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

## <a name="chapter-10---create-the-sceneorganiser-class"></a><span data-ttu-id="73331-373">Chapitre 10-créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="73331-373">Chapter 10 - Create the SceneOrganiser class</span></span>

<span data-ttu-id="73331-374">Cette classe effectuera les opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="73331-374">This class will:</span></span>

-   <span data-ttu-id="73331-375">Créez un objet **curseur** à attacher à l’appareil photo principal.</span><span class="sxs-lookup"><span data-stu-id="73331-375">Create a **Cursor** object to attach to the Main Camera.</span></span>

-   <span data-ttu-id="73331-376">Créez un objet **étiquette** qui s’affiche lorsque le service reconnaît les objets réels.</span><span class="sxs-lookup"><span data-stu-id="73331-376">Create a **Label** object that will appear when the Service recognizes the real-world objects.</span></span>

-   <span data-ttu-id="73331-377">Configurez la caméra principale en y joignant les composants appropriés.</span><span class="sxs-lookup"><span data-stu-id="73331-377">Set up the Main Camera by attaching the appropriate components to it.</span></span>

-   <span data-ttu-id="73331-378">En **mode analyse**, générez les étiquettes au moment de l’exécution, dans l’espace universel approprié par rapport à la position de la caméra principale, puis affichez les données reçues de la service vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="73331-378">When in **Analysis Mode**, spawn the Labels at runtime, in the appropriate world space relative to the position of the Main Camera, and display the data received from the Custom Vision Service.</span></span>

-   <span data-ttu-id="73331-379">En **mode d’apprentissage**, générez l’interface utilisateur qui affichera les différentes étapes du processus d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="73331-379">When in **Training Mode**, spawn the UI that will display the different stages of the training process.</span></span>

<span data-ttu-id="73331-380">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-380">To create this class:</span></span>

1.  <span data-ttu-id="73331-381">Cliquez avec le bouton droit dans le dossier **scripts** , puis cliquez sur **créer** > un**script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-381">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="73331-382">Nommez le script *SceneOrganiser*.</span><span class="sxs-lookup"><span data-stu-id="73331-382">Name the script *SceneOrganiser*.</span></span>

2.  <span data-ttu-id="73331-383">Double-cliquez sur le nouveau script *SceneOrganiser* pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-383">Double-click on the new *SceneOrganiser* script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="73331-384">Vous n’aurez besoin que d’un seul espace de noms, supprimez les autres au-dessus de la classe *SceneOrganiser* :</span><span class="sxs-lookup"><span data-stu-id="73331-384">You will only need one namespace, remove the others from above the *SceneOrganiser* class:</span></span>

    ```csharp
    using UnityEngine;
    ```

4.  <span data-ttu-id="73331-385">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *SceneOrganiser* , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="73331-385">Then add the following variables inside the *SceneOrganiser* class, above the **Start()** method:</span></span>

    ```csharp
        /// <summary>
        /// Allows this class to behave like a singleton
        /// </summary>
        public static SceneOrganiser Instance;

        /// <summary>
        /// The cursor object attached to the camera
        /// </summary>
        internal GameObject cursor;

        /// <summary>
        /// The label used to display the analysis on the objects in the real world
        /// </summary>
        internal GameObject label;

        /// <summary>
        /// Object providing the current status of the camera.
        /// </summary>
        internal TextMesh cameraStatusIndicator;

        /// <summary>
        /// Reference to the last label positioned
        /// </summary>
        internal Transform lastLabelPlaced;

        /// <summary>
        /// Reference to the last label positioned
        /// </summary>
        internal TextMesh lastLabelPlacedText;

        /// <summary>
        /// Current threshold accepted for displaying the label
        /// Reduce this value to display the recognition more often
        /// </summary>
        internal float probabilityThreshold = 0.5f;
    ```

5.  <span data-ttu-id="73331-386">Supprimez les méthodes **Start ()** et **Update ()** .</span><span class="sxs-lookup"><span data-stu-id="73331-386">Delete the **Start()** and **Update()** methods.</span></span>

6.  <span data-ttu-id="73331-387">Juste en dessous des variables, ajoutez la méthode **éveillé ()** , qui initialisera la classe et configurera la scène.</span><span class="sxs-lookup"><span data-stu-id="73331-387">Right underneath the variables, add the **Awake()** method, which will initialize the class and set up the scene.</span></span>

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            // Use this class instance as singleton
            Instance = this;

            // Add the ImageCapture class to this GameObject
            gameObject.AddComponent<ImageCapture>();

            // Add the CustomVisionAnalyser class to this GameObject
            gameObject.AddComponent<CustomVisionAnalyser>();

            // Add the CustomVisionTrainer class to this GameObject
            gameObject.AddComponent<CustomVisionTrainer>();

            // Add the VoiceRecogniser class to this GameObject
            gameObject.AddComponent<VoiceRecognizer>();

            // Add the CustomVisionObjects class to this GameObject
            gameObject.AddComponent<CustomVisionObjects>();

            // Create the camera Cursor
            cursor = CreateCameraCursor();

            // Load the label prefab as reference
            label = CreateLabel();

            // Create the camera status indicator label, and place it above where predictions
            // and training UI will appear.
            cameraStatusIndicator = CreateTrainingUI("Status Indicator", 0.02f, 0.2f, 3, true);

            // Set camera status indicator to loading.
            SetCameraStatus("Loading");
        }
    ```

7.  <span data-ttu-id="73331-388">Ajoutez à présent la méthode **CreateCameraCursor ()** qui crée et positionne le curseur principal de l’appareil photo, et la méthode **CreateLabel ()** , qui crée l’objet **étiquette d’analyse** .</span><span class="sxs-lookup"><span data-stu-id="73331-388">Now add the **CreateCameraCursor()** method that creates and positions the Main Camera cursor, and the **CreateLabel()** method, which creates the **Analysis Label** object.</span></span>

    ```csharp
        /// <summary>
        /// Spawns cursor for the Main Camera
        /// </summary>
        private GameObject CreateCameraCursor()
        {
            // Create a sphere as new cursor
            GameObject newCursor = GameObject.CreatePrimitive(PrimitiveType.Sphere);

            // Attach it to the camera
            newCursor.transform.parent = gameObject.transform;

            // Resize the new cursor
            newCursor.transform.localScale = new Vector3(0.02f, 0.02f, 0.02f);

            // Move it to the correct position
            newCursor.transform.localPosition = new Vector3(0, 0, 4);

            // Set the cursor color to red
            newCursor.GetComponent<Renderer>().material = new Material(Shader.Find("Diffuse"));
            newCursor.GetComponent<Renderer>().material.color = Color.green;

            return newCursor;
        }

        /// <summary>
        /// Create the analysis label object
        /// </summary>
        private GameObject CreateLabel()
        {
            // Create a sphere as new cursor
            GameObject newLabel = new GameObject();

            // Resize the new cursor
            newLabel.transform.localScale = new Vector3(0.01f, 0.01f, 0.01f);

            // Creating the text of the label
            TextMesh t = newLabel.AddComponent<TextMesh>();
            t.anchor = TextAnchor.MiddleCenter;
            t.alignment = TextAlignment.Center;
            t.fontSize = 50;
            t.text = "";

            return newLabel;
        }
    ```

8. <span data-ttu-id="73331-389">Ajoutez la méthode **SetCameraStatus ()** , qui gérera les messages destinés à la maille de texte qui fournit l’état de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="73331-389">Add the **SetCameraStatus()** method, which will handle messages intended for the text mesh providing the status of the camera.</span></span>

    ```csharp
        /// <summary>
        /// Set the camera status to a provided string. Will be coloured if it matches a keyword.
        /// </summary>
        /// <param name="statusText">Input string</param>
        public void SetCameraStatus(string statusText)
        {
            if (string.IsNullOrEmpty(statusText) == false)
            {
                string message = "white";

                switch (statusText.ToLower())
                {
                    case "loading":
                        message = "yellow";
                        break;

                    case "ready":
                        message = "green";
                        break;

                    case "uploading image":
                        message = "red";
                        break;

                    case "looping capture":
                        message = "yellow";
                        break;

                    case "analysis":
                        message = "red";
                        break;
                }

                cameraStatusIndicator.GetComponent<TextMesh>().text = $"Camera Status:\n<color={message}>{statusText}..</color>";
            }
        }
    ```

9. <span data-ttu-id="73331-390">Ajoutez les méthodes **PlaceAnalysisLabel ()** et **SetTagsToLastLabel ()** , qui génèrent et affichent les données de la service vision personnalisée dans la scène.</span><span class="sxs-lookup"><span data-stu-id="73331-390">Add the **PlaceAnalysisLabel()** and **SetTagsToLastLabel()** methods, which will spawn and display the data from the Custom Vision Service into the scene.</span></span>

    ```csharp
        /// <summary>
        /// Instantiate a label in the appropriate location relative to the Main Camera.
        /// </summary>
        public void PlaceAnalysisLabel()
        {
            lastLabelPlaced = Instantiate(label.transform, cursor.transform.position, transform.rotation);
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();
        }

        /// <summary>
        /// Set the Tags as Text of the last label created. 
        /// </summary>
        public void SetTagsToLastLabel(AnalysisObject analysisObject)
        {
            lastLabelPlacedText = lastLabelPlaced.GetComponent<TextMesh>();

            if (analysisObject.Predictions != null)
            {
                foreach (Prediction p in analysisObject.Predictions)
                {
                    if (p.Probability > 0.02)
                    {
                        lastLabelPlacedText.text += $"Detected: {p.TagName} {p.Probability.ToString("0.00 \n")}";
                        Debug.Log($"Detected: {p.TagName} {p.Probability.ToString("0.00 \n")}");
                    }
                }
            }
        }
    ```

10. <span data-ttu-id="73331-391">Enfin, ajoutez la méthode **CreateTrainingUI ()** , qui générera l’interface utilisateur en affichant les différentes étapes du processus d’apprentissage lorsque l’application est en mode d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="73331-391">Lastly, add the **CreateTrainingUI()** method, which will spawn the UI displaying the multiple stages of the training process when the application is in Training Mode.</span></span> <span data-ttu-id="73331-392">Cette méthode est également exploitable pour créer l’objet d’état de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="73331-392">This method will also be harnessed to create the camera status object.</span></span>

    ```csharp
        /// <summary>
        /// Create a 3D Text Mesh in scene, with various parameters.
        /// </summary>
        /// <param name="name">name of object</param>
        /// <param name="scale">scale of object (i.e. 0.04f)</param>
        /// <param name="yPos">height above the cursor (i.e. 0.3f</param>
        /// <param name="zPos">distance from the camera</param>
        /// <param name="setActive">whether the text mesh should be visible when it has been created</param>
        /// <returns>Returns a 3D text mesh within the scene</returns>
        internal TextMesh CreateTrainingUI(string name, float scale, float yPos, float zPos, bool setActive)
        {
            GameObject display = new GameObject(name, typeof(TextMesh));
            display.transform.parent = Camera.main.transform;
            display.transform.localPosition = new Vector3(0, yPos, zPos);
            display.SetActive(setActive);
            display.transform.localScale = new Vector3(scale, scale, scale);
            display.transform.rotation = new Quaternion();
            TextMesh textMesh = display.GetComponent<TextMesh>();
            textMesh.anchor = TextAnchor.MiddleCenter;
            textMesh.alignment = TextAlignment.Center;
            return textMesh;
        }
    ```

11. <span data-ttu-id="73331-393">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-393">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="73331-394">Avant de continuer, ouvrez la classe **CustomVisionAnalyser** et, dans la méthode **AnalyseLastImageCaptured ()** , *supprimez les marques de commentaire* des lignes suivantes:</span><span class="sxs-lookup"><span data-stu-id="73331-394">Before you continue, open the **CustomVisionAnalyser** class, and within the **AnalyseLastImageCaptured()** method, *uncomment* the following lines:</span></span>
>
> ```csharp
>   AnalysisObject analysisObject = new AnalysisObject();
>   analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
>   SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
> ```

## <a name="chapter-11---create-the-imagecapture-class"></a><span data-ttu-id="73331-395">Chapitre 11-créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="73331-395">Chapter 11 - Create the ImageCapture class</span></span>

<span data-ttu-id="73331-396">La classe suivante que vous allez créer est la classe *ImageCapture* .</span><span class="sxs-lookup"><span data-stu-id="73331-396">The next class you are going to create is the *ImageCapture* class.</span></span>

<span data-ttu-id="73331-397">Cette classe est chargée des opérations suivantes:</span><span class="sxs-lookup"><span data-stu-id="73331-397">This class is responsible for:</span></span>

-   <span data-ttu-id="73331-398">Capture d’une image à l’aide de la caméra HoloLens et stockage dans le dossier de l' *application* .</span><span class="sxs-lookup"><span data-stu-id="73331-398">Capturing an image using the HoloLens camera and storing it in the *App* Folder.</span></span>

-   <span data-ttu-id="73331-399">Gestion des gestes TAP de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="73331-399">Handling Tap gestures from the user.</span></span>

-   <span data-ttu-id="73331-400">Maintien de la valeur *enum* qui détermine si l’application s’exécutera en mode d' *analyse* ou en mode d' *apprentissage* .</span><span class="sxs-lookup"><span data-stu-id="73331-400">Maintaining the *Enum* value that determines if the application will run in *Analysis* mode or *Training* Mode.</span></span>

<span data-ttu-id="73331-401">Pour créer cette classe:</span><span class="sxs-lookup"><span data-stu-id="73331-401">To create this class:</span></span>

1.  <span data-ttu-id="73331-402">Accédez au dossier **scripts** que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="73331-402">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="73331-403">Cliquez avec le bouton droit dans le dossier, puis cliquez sur **créer > script C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-403">Right-click inside the folder, then click **Create > C\# Script**.</span></span> <span data-ttu-id="73331-404">Nommez le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="73331-404">Name the script *ImageCapture*.</span></span>

3.  <span data-ttu-id="73331-405">Double-cliquez sur le nouveau script **ImageCapture** pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-405">Double-click on the new **ImageCapture** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="73331-406">Remplacez les espaces de noms en haut du fichier par les éléments suivants:</span><span class="sxs-lookup"><span data-stu-id="73331-406">Replace the namespaces at the top of the file with the following:</span></span>

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="73331-407">Ajoutez ensuite les variables suivantes à l’intérieur de la classe *ImageCapture* , au-dessus de la méthode **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="73331-407">Then add the following variables inside the *ImageCapture* class, above the **Start()** method:</span></span>

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
        /// Loop timer
        /// </summary>
        private float secondsBetweenCaptures = 10f;

        /// <summary>
        /// Application main functionalities switch
        /// </summary>
        internal enum AppModes {Analysis, Training }
        
        /// <summary>
        /// Local variable for current AppMode
        /// </summary>
        internal AppModes AppMode { get; private set; }

        /// <summary>
        /// Flagging if the capture loop is running
        /// </summary>
        internal bool captureIsActive;
        
        /// <summary>
        /// File path of current analysed photo
        /// </summary>
        internal string filePath = string.Empty;
    ```

6.  <span data-ttu-id="73331-408">Vous devez maintenant ajouter le code des méthodes **éveillés ()** et **Start ()** :</span><span class="sxs-lookup"><span data-stu-id="73331-408">Code for **Awake()** and **Start()** methods now needs to be added:</span></span>

    ```csharp
        /// <summary>
        /// Called on initialization
        /// </summary>
        private void Awake()
        {
            Instance = this;

            // Change this flag to switch between Analysis Mode and Training Mode 
            AppMode = AppModes.Training;
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

            // Subscribing to the Hololens API gesture recognizer to track user gestures
            recognizer = new GestureRecognizer();
            recognizer.SetRecognizableGestures(GestureSettings.Tap);
            recognizer.Tapped += TapHandler;
            recognizer.StartCapturingGestures();

            SceneOrganiser.Instance.SetCameraStatus("Ready");
        }
    ```

7.  <span data-ttu-id="73331-409">Implémentez un gestionnaire qui sera appelé quand un mouvement TAP se produit.</span><span class="sxs-lookup"><span data-stu-id="73331-409">Implement a handler that will be called when a Tap gesture occurs.</span></span>

    ```csharp
        /// <summary>
        /// Respond to Tap Input.
        /// </summary>
        private void TapHandler(TappedEventArgs obj)
        {
            switch (AppMode)
            {
                case AppModes.Analysis:
                    if (!captureIsActive)
                    {
                        captureIsActive = true;

                        // Set the cursor color to red
                        SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;
                        
                        // Update camera status to looping capture.
                        SceneOrganiser.Instance.SetCameraStatus("Looping Capture");

                        // Begin the capture loop
                        InvokeRepeating("ExecuteImageCaptureAndAnalysis", 0, secondsBetweenCaptures);
                    }
                    else
                    {
                        // The user tapped while the app was analyzing 
                        // therefore stop the analysis process
                        ResetImageCapture();
                    }
                    break;

                case AppModes.Training:
                    if (!captureIsActive)
                    {
                        captureIsActive = true;

                        // Call the image capture
                        ExecuteImageCaptureAndAnalysis();

                        // Set the cursor color to red
                        SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.red;

                        // Update camera status to uploading image.
                        SceneOrganiser.Instance.SetCameraStatus("Uploading Image");
                    }              
                    break;
            }     
        }
    ```

    > [!NOTE] 
    > <span data-ttu-id="73331-410">En mode *analyse* , la méthode **TapHandler** agit comme un commutateur pour démarrer ou arrêter la boucle de capture photo.</span><span class="sxs-lookup"><span data-stu-id="73331-410">In *Analysis* mode, the **TapHandler** method acts as a switch to start or stop the photo capture loop.</span></span>
    >
    > <span data-ttu-id="73331-411">En mode d' *apprentissage* , une image est capturée à partir de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="73331-411">In *Training* mode, it will capture an image from the camera.</span></span>
    >
    > <span data-ttu-id="73331-412">Lorsque le curseur est vert, cela signifie que l’appareil photo est disponible pour prendre l’image.</span><span class="sxs-lookup"><span data-stu-id="73331-412">When the cursor is green, it means the camera is available to take the image.</span></span>
    >
    > <span data-ttu-id="73331-413">Lorsque le curseur est rouge, cela signifie que l’appareil photo est occupé.</span><span class="sxs-lookup"><span data-stu-id="73331-413">When the cursor is red, it means the camera is busy.</span></span>

8.  <span data-ttu-id="73331-414">Ajoutez la méthode utilisée par l’application pour démarrer le processus de capture d’image et stocker l’image.</span><span class="sxs-lookup"><span data-stu-id="73331-414">Add the method that the application uses to start the image capture process and store the image.</span></span>

    ```csharp
        /// <summary>
        /// Begin process of Image Capturing and send To Azure Custom Vision Service.
        /// </summary>
        private void ExecuteImageCaptureAndAnalysis()
        {
            // Update camera status to analysis.
            SceneOrganiser.Instance.SetCameraStatus("Analysis");

            // Create a label in world space using the SceneOrganiser class 
            // Invisible at this point but correctly positioned where the image was taken
            SceneOrganiser.Instance.PlaceAnalysisLabel();

            // Set the camera resolution to be the highest possible
            Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();

            Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);

            // Begin capture process, set the image format
            PhotoCapture.CreateAsync(false, delegate (PhotoCapture captureObject)
            {
                photoCaptureObject = captureObject;

                CameraParameters camParameters = new CameraParameters
                {
                    hologramOpacity = 0.0f,
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

9.  <span data-ttu-id="73331-415">Ajoutez les gestionnaires qui seront appelés lorsque la photo a été capturée et le moment où elle sera prête à être analysée.</span><span class="sxs-lookup"><span data-stu-id="73331-415">Add the handlers that will be called when the photo has been captured and for when it is ready to be analyzed.</span></span> <span data-ttu-id="73331-416">Le résultat est ensuite transmis à *CustomVisionAnalyser* ou *CustomVisionTrainer* selon le mode sur lequel le code est défini.</span><span class="sxs-lookup"><span data-stu-id="73331-416">The result is then passed to the *CustomVisionAnalyser* or the *CustomVisionTrainer* depending on which mode the code is set on.</span></span>

    ```csharp
        /// <summary>
        /// Register the full execution of the Photo Capture. 
        /// </summary>
        void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
        {
                // Call StopPhotoMode once the image has successfully captured
                photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
        }


        /// <summary>
        /// The camera photo mode has stopped after the capture.
        /// Begin the Image Analysis process.
        /// </summary>
        void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
        {
            Debug.LogFormat("Stopped Photo Mode");
        
            // Dispose from the object in memory and request the image analysis 
            photoCaptureObject.Dispose();
            photoCaptureObject = null;

            switch (AppMode)
            {
                case AppModes.Analysis:
                    // Call the image analysis
                    StartCoroutine(CustomVisionAnalyser.Instance.AnalyseLastImageCaptured(filePath));
                    break;

                case AppModes.Training:
                    // Call training using captured image
                    CustomVisionTrainer.Instance.RequestTagSelection();
                    break;
            }
        }

        /// <summary>
        /// Stops all capture pending actions
        /// </summary>
        internal void ResetImageCapture()
        {
            captureIsActive = false;

            // Set the cursor color to green
            SceneOrganiser.Instance.cursor.GetComponent<Renderer>().material.color = Color.green;

            // Update camera status to ready.
            SceneOrganiser.Instance.SetCameraStatus("Ready");

            // Stop the capture loop if active
            CancelInvoke();
        }
    ```

10. <span data-ttu-id="73331-417">Veillez à enregistrer vos modifications dans **Visual Studio** avant de revenir à Unity.</span><span class="sxs-lookup"><span data-stu-id="73331-417">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

11. <span data-ttu-id="73331-418">Maintenant que tous les scripts ont été exécutés, revenez dans l’éditeur Unity, puis cliquez et faites glisser la classe **SceneOrganiser** du dossier **scripts** vers l’objet **Camera principal** dans le *panneau hiérarchie*.</span><span class="sxs-lookup"><span data-stu-id="73331-418">Now that all the scripts have been completed, go back in the Unity Editor, then click and drag the **SceneOrganiser** class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

## <a name="chapter-12---before-building"></a><span data-ttu-id="73331-419">Chapitre 12-avant génération</span><span class="sxs-lookup"><span data-stu-id="73331-419">Chapter 12 - Before building</span></span>

<span data-ttu-id="73331-420">Pour effectuer un test minutieux de votre application, vous devez l’chargement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="73331-420">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>

<span data-ttu-id="73331-421">Avant cela, assurez-vous que:</span><span class="sxs-lookup"><span data-stu-id="73331-421">Before you do, ensure that:</span></span>

- <span data-ttu-id="73331-422">Tous les paramètres mentionnés dans le [Chapitre 2](#chapter-2---training-your-custom-vision-project) sont correctement définis.</span><span class="sxs-lookup"><span data-stu-id="73331-422">All the settings mentioned in the [Chapter 2](#chapter-2---training-your-custom-vision-project) are set correctly.</span></span>

- <span data-ttu-id="73331-423">Tous les champs de l' **appareil photo principal**, du panneau Inspecteur, sont correctement affectés.</span><span class="sxs-lookup"><span data-stu-id="73331-423">All the fields in the **Main Camera**, Inspector Panel, are assigned properly.</span></span>

- <span data-ttu-id="73331-424">Le script **SceneOrganiser** est attaché à l’objet **Camera principal** .</span><span class="sxs-lookup"><span data-stu-id="73331-424">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span>

- <span data-ttu-id="73331-425">Veillez à insérer votre **clé** de prédiction dans la variable **predictionKey** .</span><span class="sxs-lookup"><span data-stu-id="73331-425">Make sure you insert your **Prediction Key** into the **predictionKey** variable.</span></span>

- <span data-ttu-id="73331-426">Vous avez inséré votre **point de terminaison** de prédiction dans la variable **predictionEndpoint** .</span><span class="sxs-lookup"><span data-stu-id="73331-426">You have inserted your **Prediction Endpoint** into the **predictionEndpoint** variable.</span></span>

- <span data-ttu-id="73331-427">Vous avez inséré votre **clé de formation** dans la variable **trainingKey** de la classe *CustomVisionTrainer* .</span><span class="sxs-lookup"><span data-stu-id="73331-427">You have inserted your **Training Key** into the **trainingKey** variable, of the *CustomVisionTrainer* class.</span></span>

- <span data-ttu-id="73331-428">Vous avez inséré votre **ID de projet** dans la variable **ProjectId** de la classe *CustomVisionTrainer* .</span><span class="sxs-lookup"><span data-stu-id="73331-428">You have inserted your **Project ID** into the **projectId** variable, of the *CustomVisionTrainer* class.</span></span>

## <a name="chapter-13---build-and-sideload-your-application"></a><span data-ttu-id="73331-429">Chapitre 13-créer et chargement votre application</span><span class="sxs-lookup"><span data-stu-id="73331-429">Chapter 13 - Build and sideload your application</span></span>

<span data-ttu-id="73331-430">Pour commencer le processus de *génération* :</span><span class="sxs-lookup"><span data-stu-id="73331-430">To begin the *Build* process:</span></span>

1.  <span data-ttu-id="73331-431">Accédez à **fichier > paramètres de build**.</span><span class="sxs-lookup"><span data-stu-id="73331-431">Go to **File > Build Settings**.</span></span>

2.  <span data-ttu-id="73331-432">**Projets Tick Unity C\#** .</span><span class="sxs-lookup"><span data-stu-id="73331-432">Tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="73331-433">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="73331-433">Click **Build**.</span></span> <span data-ttu-id="73331-434">Unity lance une fenêtre de l' **Explorateur de fichiers** , dans laquelle vous devez créer, puis sélectionner un dossier dans lequel générer l’application.</span><span class="sxs-lookup"><span data-stu-id="73331-434">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="73331-435">Créez ce dossier maintenant, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="73331-435">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="73331-436">Ensuite, avec le dossier d' **application** sélectionné, cliquez sur **Sélectionner un dossier**.</span><span class="sxs-lookup"><span data-stu-id="73331-436">Then with the **App** folder selected, click on **Select Folder**.</span></span>

4.  <span data-ttu-id="73331-437">Unity commence à générer votre projet dans le dossier de l' **application** .</span><span class="sxs-lookup"><span data-stu-id="73331-437">Unity will begin building your project to the **App** folder.</span></span>

5.  <span data-ttu-id="73331-438">Une fois la génération de Unity terminée (cela peut prendre un certain temps), une fenêtre de l' **Explorateur de fichiers** s’ouvre à l’emplacement de votre Build (Vérifiez la barre des tâches, car elle ne s’affiche pas toujours au-dessus de votre Windows, mais vous informera de l’ajout d’une nouvelle fenêtre).</span><span class="sxs-lookup"><span data-stu-id="73331-438">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

<span data-ttu-id="73331-439">Pour effectuer un déploiement sur HoloLens:</span><span class="sxs-lookup"><span data-stu-id="73331-439">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="73331-440">Vous aurez besoin de l’adresse IP de votre HoloLens (pour le déploiement à distance) et vérifiez que votre HoloLens est en **mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="73331-440">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="73331-441">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="73331-441">To do this:</span></span>

    1.  <span data-ttu-id="73331-442">Tout en portant votre HoloLens, ouvrez les **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="73331-442">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="73331-443">Accéder au **réseau &**  > **Options avancées** **de Wi-Fi** > Internet</span><span class="sxs-lookup"><span data-stu-id="73331-443">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="73331-444">Notez l’adresse **IPv4** .</span><span class="sxs-lookup"><span data-stu-id="73331-444">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="73331-445">Ensuite, revenez aux **paramètres**, puis pour **mettre à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="73331-445">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="73331-446">Définissez **le mode développeur sur**.</span><span class="sxs-lookup"><span data-stu-id="73331-446">Set **Developer Mode On**.</span></span>

2.  <span data-ttu-id="73331-447">Accédez à votre nouvelle build Unity (le dossier de l' **application** ) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="73331-447">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

3.  <span data-ttu-id="73331-448">Dans la *configuration* de la solution, sélectionnez Déboguer.</span><span class="sxs-lookup"><span data-stu-id="73331-448">In the *Solution Configuration* select **Debug**.</span></span>

4.  <span data-ttu-id="73331-449">Dans la *plateforme*de la solution, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="73331-449">In the *Solution Platform*, select **x86, Remote Machine**.</span></span> <span data-ttu-id="73331-450">Vous serez invité à insérer l' **adresse IP** d’un périphérique distant (le HoloLens, dans ce cas, que vous avez noté).</span><span class="sxs-lookup"><span data-stu-id="73331-450">You will be prompted to insert the **IP address** of a remote device (the HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab302b-34.png)

5. <span data-ttu-id="73331-451">Accédez au menu **générer** , puis cliquez sur **déployer la solution** pour chargement l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="73331-451">Go to **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

6. <span data-ttu-id="73331-452">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prête à être lancée.</span><span class="sxs-lookup"><span data-stu-id="73331-452">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="73331-453">Pour effectuer un déploiement sur un casque immersif, définissez la plateforme de la **solution** sur *ordinateur local*et définissez la **configuration** sur déboguer, avec *x86* comme **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="73331-453">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="73331-454">Déployez ensuite sur l’ordinateur local, à l’aide de l’élément de menu **générer** , en sélectionnant *déployer la solution*.</span><span class="sxs-lookup"><span data-stu-id="73331-454">Then deploy to the local machine, using the **Build** menu item, selecting *Deploy Solution*.</span></span> 

## <a name="to-use-the-application"></a><span data-ttu-id="73331-455">Pour utiliser l’application:</span><span class="sxs-lookup"><span data-stu-id="73331-455">To use the application:</span></span>

<span data-ttu-id="73331-456">Pour basculer la fonctionnalité de l’application entre le mode d' *apprentissage* et le mode de prédiction, vous devez mettre à jour la variable **AppMode** , située dans la méthode  **éveillé ()** située dans la classe *ImageCapture* .</span><span class="sxs-lookup"><span data-stu-id="73331-456">To switch the app functionality between *Training* mode and *Prediction* mode you need to update the **AppMode** variable, located in the **Awake()** method located within the *ImageCapture* class.</span></span>

```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Training;
```
<span data-ttu-id="73331-457">ou Gestionnaire de configuration</span><span class="sxs-lookup"><span data-stu-id="73331-457">or</span></span>
```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Analysis;
```

<span data-ttu-id="73331-458">En mode d' *apprentissage* :</span><span class="sxs-lookup"><span data-stu-id="73331-458">In *Training* mode:</span></span>

- <span data-ttu-id="73331-459">Regardez la **souris** ou le **clavier** et utilisez le **mouvement TAP**.</span><span class="sxs-lookup"><span data-stu-id="73331-459">Look at **Mouse** or **Keyboard** and use the **Tap gesture**.</span></span>

- <span data-ttu-id="73331-460">Ensuite, du texte s’affiche pour vous demander de fournir une balise.</span><span class="sxs-lookup"><span data-stu-id="73331-460">Next, text will appear asking you to provide a tag.</span></span>

- <span data-ttu-id="73331-461">Disons **la souris** ou le **clavier**.</span><span class="sxs-lookup"><span data-stu-id="73331-461">Say either **Mouse** or **Keyboard**.</span></span>


<span data-ttu-id="73331-462">En  mode de prédiction:</span><span class="sxs-lookup"><span data-stu-id="73331-462">In *Prediction* mode:</span></span>

- <span data-ttu-id="73331-463">Examinez un objet et utilisez le **mouvement TAP**.</span><span class="sxs-lookup"><span data-stu-id="73331-463">Look at an object and use the **Tap gesture**.</span></span>

- <span data-ttu-id="73331-464">Du texte s’affiche pour indiquer l’objet détecté, avec la probabilité la plus élevée (cette opération est normalisée).</span><span class="sxs-lookup"><span data-stu-id="73331-464">Text will appear providing the object detected, with the highest probability (this is normalized).</span></span>

## <a name="chapter-14---evaluate-and-improve-your-custom-vision-model"></a><span data-ttu-id="73331-465">Chapitre 14-évaluer et améliorer votre modèle de Custom Vision</span><span class="sxs-lookup"><span data-stu-id="73331-465">Chapter 14 - Evaluate and improve your Custom Vision model</span></span>

<span data-ttu-id="73331-466">Pour améliorer la précision de votre service, vous devrez continuer à former le modèle utilisé pour la prédiction.</span><span class="sxs-lookup"><span data-stu-id="73331-466">To make your Service more accurate, you will need to continue to train the model used for prediction.</span></span> <span data-ttu-id="73331-467">Pour ce faire, vous pouvez utiliser votre nouvelle application, à la fois avec les modes de *formation* et de prédiction, avec ceux qui vous demandent de visiter le portail, ce qui est abordé dans ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="73331-467">This is accomplished through using your new application, with both the *training* and *prediction* modes, with the latter requiring you to visit the portal, which is what is covered in this Chapter.</span></span> <span data-ttu-id="73331-468">Préparez-vous à revisiter votre portail plusieurs fois, afin d’améliorer continuellement votre modèle.</span><span class="sxs-lookup"><span data-stu-id="73331-468">Be prepared to revisit your portal many times, to continually improve your model.</span></span>

1. <span data-ttu-id="73331-469">Accédez à nouveau à votre portail Azure Custom Vision et, une fois que vous êtes dans votre projet  , sélectionnez l’onglet prédictions (à partir du centre en haut de la page):</span><span class="sxs-lookup"><span data-stu-id="73331-469">Head to your Azure Custom Vision Portal again, and once you are in your project, select the *Predictions* tab (from the top center of the page):</span></span>

    ![](images/AzureLabs-Lab302b-35.png)

2. <span data-ttu-id="73331-470">Vous verrez toutes les images qui ont été envoyées à votre service pendant l’exécution de votre application.</span><span class="sxs-lookup"><span data-stu-id="73331-470">You will see all the images which were sent to your Service whilst your application was running.</span></span> <span data-ttu-id="73331-471">Si vous pointez sur les images, elles vous fourniront les prédictions qui ont été effectuées pour cette image:</span><span class="sxs-lookup"><span data-stu-id="73331-471">If you hover over the images, they will provide you with the predictions that were made for that image:</span></span>

    ![](images/AzureLabs-Lab302b-36.png)

3. <span data-ttu-id="73331-472">Sélectionnez l’une de vos images pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="73331-472">Select one of your images to open it.</span></span> <span data-ttu-id="73331-473">Une fois ouvert, vous verrez les prédictions effectuées pour cette image à droite.</span><span class="sxs-lookup"><span data-stu-id="73331-473">Once open, you will see the predictions made for that image to the right.</span></span> <span data-ttu-id="73331-474">Si les prédictions sont correctes et que vous souhaitez ajouter cette image au modèle d’apprentissage de votre service, cliquez sur la zone de texte *mes balises* , puis sélectionnez la balise que vous souhaitez associer.</span><span class="sxs-lookup"><span data-stu-id="73331-474">If you the predictions were correct, and you wish to add this image to your Service's training model, click the *My Tags* input box, and select the tag you wish to associate.</span></span> <span data-ttu-id="73331-475">Lorsque vous avez terminé, cliquez sur le bouton *enregistrer et fermer* en bas à droite, puis passez à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="73331-475">When you are finished, click the *Save and close* button to the bottom right, and continue on to the next image.</span></span>

    ![](images/AzureLabs-Lab302b-37.png)

4. <span data-ttu-id="73331-476">Une fois que vous revenez à la grille des images, vous remarquerez que les images auxquelles vous avez ajouté des balises (et enregistrées) seront supprimées.</span><span class="sxs-lookup"><span data-stu-id="73331-476">Once you are back to the grid of images, you will notice the images which you have added tags to (and saved), will be removed.</span></span> <span data-ttu-id="73331-477">Si vous trouvez des images dont vous pensez que vous n’avez pas besoin de votre élément balisé, vous pouvez les supprimer en cliquant sur le bouton de l’image (cette opération peut s’effectuer pour plusieurs images), puis en cliquant sur *supprimer* dans le coin supérieur droit de la page de grille.</span><span class="sxs-lookup"><span data-stu-id="73331-477">If you find any images which you think do not have your tagged item within them, you can delete them, by clicking the tick on that image (can do this for several images) and then clicking *Delete* in the upper right corner of the grid page.</span></span> <span data-ttu-id="73331-478">Dans le menu contextuel qui suit, vous pouvez cliquer sur *Oui, supprimer* ou *non*pour confirmer la suppression ou l’annuler, respectivement.</span><span class="sxs-lookup"><span data-stu-id="73331-478">On the popup that follows, you can click either *Yes, delete* or *No*, to confirm the deletion or cancel it, respectively.</span></span> 

    ![](images/AzureLabs-Lab302b-38.png)

5. <span data-ttu-id="73331-479">Lorsque vous êtes prêt à continuer, cliquez sur le bouton vert *train* en haut à droite.</span><span class="sxs-lookup"><span data-stu-id="73331-479">When you are ready to proceed, click the green *Train* button in the top right.</span></span> <span data-ttu-id="73331-480">Votre modèle de service sera formé avec toutes les images que vous avez fournies (ce qui le rendra plus précis).</span><span class="sxs-lookup"><span data-stu-id="73331-480">Your Service model will be trained with all the images which you have now provided (which will make it more accurate).</span></span> <span data-ttu-id="73331-481">Une fois l’apprentissage terminé, veillez à cliquer une fois de plus sur le bouton *créer par défaut* , afin que votre *URL* de prédiction continue à utiliser l’itération la plus récente de votre service.</span><span class="sxs-lookup"><span data-stu-id="73331-481">Once the training is complete, make sure to click the *Make default* button once more, so that your *Prediction URL* continues to use the most up-to-date iteration of your Service.</span></span>

    <span data-ttu-id="73331-482">![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)</span><span class="sxs-lookup"><span data-stu-id="73331-482">![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)</span></span>

## <a name="your-finished-custom-vision-api-application"></a><span data-ttu-id="73331-483">Votre application API Custom Vision terminée</span><span class="sxs-lookup"><span data-stu-id="73331-483">Your finished Custom Vision API application</span></span>

<span data-ttu-id="73331-484">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API Azure Custom Vision pour reconnaître des objets réels, former le modèle de service et afficher la confiance de ce qui a été observé.</span><span class="sxs-lookup"><span data-stu-id="73331-484">Congratulations, you built a mixed reality app that leverages the Azure Custom Vision API to recognize real world objects, train the Service model, and display confidence of what has been seen.</span></span>

![](images/AzureLabs-Lab302b-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="73331-485">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="73331-485">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="73331-486">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="73331-486">Exercise 1</span></span>

<span data-ttu-id="73331-487">Formez votre **service vision personnalisée** pour qu’il reconnaisse plus d’objets.</span><span class="sxs-lookup"><span data-stu-id="73331-487">Train your **Custom Vision Service** to recognize more objects.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="73331-488">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="73331-488">Exercise 2</span></span>

<span data-ttu-id="73331-489">Pour vous familiariser avec ce que vous avez appris, effectuez les exercices suivants:</span><span class="sxs-lookup"><span data-stu-id="73331-489">As a way to expand on what you have learned, complete the following exercises:</span></span>

<span data-ttu-id="73331-490">Émettre un signal sonore lorsqu’un objet est reconnu.</span><span class="sxs-lookup"><span data-stu-id="73331-490">Play a sound when an object is recognized.</span></span>

### <a name="exercise-3"></a><span data-ttu-id="73331-491">Exercice 3</span><span class="sxs-lookup"><span data-stu-id="73331-491">Exercise 3</span></span>

<span data-ttu-id="73331-492">Utilisez l’API pour reformer votre service avec les mêmes images que celles que votre application analyse, afin de rendre le service plus précis (effectuer la prédiction et la formation simultanément).</span><span class="sxs-lookup"><span data-stu-id="73331-492">Use the API to re-train your Service with the same images your app is analyzing, so to make the Service more accurate (do both prediction and training simultaneously).</span></span>
