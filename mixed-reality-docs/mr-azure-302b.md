---
title: MR et 302b Azure - vision personnalisée
description: Terminer ce cours pour apprendre à former un modèle d’apprentissage et ensuite utiliser le modèle formé pour reconnaître des objets similaires au sein d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/03/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, unity, didacticiel, api, vision personnalisée, hololens, immersives, vr
ms.openlocfilehash: e6e9782a8d559af660dc4765556f1e926c5360b1
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59594226"
---
>[!NOTE]
><span data-ttu-id="c0e30-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="c0e30-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="c0e30-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="c0e30-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="c0e30-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="c0e30-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="c0e30-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="c0e30-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="c0e30-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="c0e30-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="c0e30-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="c0e30-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

<br>

# <a name="mr-and-azure-302b-custom-vision"></a><span data-ttu-id="c0e30-110">MR et 302b Azure : Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-110">MR and Azure 302b: Custom vision</span></span>

<span data-ttu-id="c0e30-111">Dans ce cours, vous allez apprendre à reconnaître un contenu visuel personnalisé au sein d’une image fournie, à l’aide des fonctionnalités de Vision personnalisée d’Azure dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="c0e30-111">In this course, you will learn how to recognize custom visual content within a provided image, using Azure Custom Vision capabilities in a mixed reality application.</span></span>

<span data-ttu-id="c0e30-112">Ce service vous permettra de former un modèle d’apprentissage automatique à l’aide d’images de l’objet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-112">This service will allow you to train a machine learning model using object images.</span></span> <span data-ttu-id="c0e30-113">Vous utiliserez ensuite le modèle formé pour reconnaître des objets semblables, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou un appareil photo connecté à votre PC pour des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="c0e30-113">You will then use the trained model to recognize similar objects, as provided by the camera capture of Microsoft HoloLens or a camera connected to your PC for immersive (VR) headsets.</span></span>

![résultat de cours](images/AzureLabs-Lab302b-00.png)

<span data-ttu-id="c0e30-115">Vision personnalisée Azure est un Service COGNITIF de Microsoft qui permet aux développeurs de créer des classifieurs de l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-115">Azure Custom Vision is a Microsoft Cognitive Service which allows developers to build custom image classifiers.</span></span> <span data-ttu-id="c0e30-116">Ces classifieurs peuvent ensuite être utilisées avec les nouvelles images pour reconnaître ou classement, d’objets au sein de cette nouvelle image.</span><span class="sxs-lookup"><span data-stu-id="c0e30-116">These classifiers can then be used with new images to recognize, or classify, objects within that new image.</span></span> <span data-ttu-id="c0e30-117">Le Service fournit un portail en ligne simple et facile à utiliser, pour simplifier le processus.</span><span class="sxs-lookup"><span data-stu-id="c0e30-117">The Service provides a simple, easy to use, online portal to streamline the process.</span></span> <span data-ttu-id="c0e30-118">Pour plus d’informations, visitez le [page de Azure Custom Vision Service](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span><span class="sxs-lookup"><span data-stu-id="c0e30-118">For more information, visit the [Azure Custom Vision Service page](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home).</span></span>

<span data-ttu-id="c0e30-119">À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure de fonctionner dans deux modes :</span><span class="sxs-lookup"><span data-stu-id="c0e30-119">Upon completion of this course, you will have a mixed reality application which will be able to work in two modes:</span></span>

-   <span data-ttu-id="c0e30-120">**Mode d’analyse**: configurer le Service Vision personnalisée manuellement par le téléchargement d’images, création de balises et le Service de formation pour reconnaître des différents objets (dans ce cas de la souris et du clavier).</span><span class="sxs-lookup"><span data-stu-id="c0e30-120">**Analysis Mode**: setting up the Custom Vision Service manually by uploading images, creating tags, and training the Service to recognize different objects (in this case mouse and keyboard).</span></span> <span data-ttu-id="c0e30-121">Vous allez ensuite créer une application de HoloLens qui capture des images à l’aide de l’appareil photo, puis réessayer d’identifier ces objets dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="c0e30-121">You will then create a HoloLens app that will capture images using the camera, and try to recognize those objects in the real world.</span></span>

-   <span data-ttu-id="c0e30-122">**Mode d’apprentissage**: vous implémentez le code qui permettra un « Mode de formation » dans votre application.</span><span class="sxs-lookup"><span data-stu-id="c0e30-122">**Training Mode**: you will implement code that will enable a "Training Mode" in your app.</span></span> <span data-ttu-id="c0e30-123">Le mode d’apprentissage vous permettra de capturer des images à l’aide de la caméra des HoloLens, charger les images capturées dans le Service et former le modèle de vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-123">The training mode will allow you to capture images using the HoloLens' camera, upload the captured images to the Service, and train the custom vision model.</span></span>

<span data-ttu-id="c0e30-124">Ce cours va vous apprendre à obtenir les résultats à partir du Service de Vision personnalisée dans une application basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-124">This course will teach you how to get the results from the Custom Vision Service into a Unity-based sample application.</span></span> <span data-ttu-id="c0e30-125">Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.</span><span class="sxs-lookup"><span data-stu-id="c0e30-125">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="c0e30-126">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="c0e30-126">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="c0e30-127">Cours</span><span class="sxs-lookup"><span data-stu-id="c0e30-127">Course</span></span></th><th style="width:150px"> <span data-ttu-id="c0e30-128"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="c0e30-128"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="c0e30-129"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="c0e30-129"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="c0e30-130">MR et 302b Azure : Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-130">MR and Azure 302b: Custom vision</span></span></td><td style="text-align: center;"> <span data-ttu-id="c0e30-131">✔️</span><span class="sxs-lookup"><span data-stu-id="c0e30-131">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="c0e30-132">✔️</span><span class="sxs-lookup"><span data-stu-id="c0e30-132">✔️</span></span></td>
</tr>
</table>

> [!NOTE]
> <span data-ttu-id="c0e30-133">Si ce cours se concentre principalement sur HoloLens, vous pouvez également appliquer ce que vous allez apprendre dans ce cours à des casques Windows Mixed Reality IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="c0e30-133">While this course primarily focuses on HoloLens, you can also apply what you learn in this course to Windows Mixed Reality immersive (VR) headsets.</span></span> <span data-ttu-id="c0e30-134">Étant donné que des casques IMMERSIFS (VR) ne sont pas accessibles caméras, vous devez une caméra externe connectée à votre PC.</span><span class="sxs-lookup"><span data-stu-id="c0e30-134">Because immersive (VR) headsets do not have accessible cameras, you will need an external camera connected to your PC.</span></span> <span data-ttu-id="c0e30-135">Que vous suivez le cours, vous verrez des notes sur les modifications que vous devrez peut-être à employer pour prendre en charge des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="c0e30-135">As you follow along with the course, you will see notes on any changes you might need to employ to support immersive (VR) headsets.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c0e30-136">Prérequis</span><span class="sxs-lookup"><span data-stu-id="c0e30-136">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="c0e30-137">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="c0e30-137">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="c0e30-138">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="c0e30-138">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="c0e30-139">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="c0e30-139">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="c0e30-140">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="c0e30-140">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="c0e30-141">Un PC, de développement [compatible avec Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) pour le développement de casque immersive (VR)</span><span class="sxs-lookup"><span data-stu-id="c0e30-141">A development PC, [compatible with Windows Mixed Reality](https://support.microsoft.com/help/4039260/windows-10-mixed-reality-pc-hardware-guidelines) for immersive (VR) headset development</span></span>
- [<span data-ttu-id="c0e30-142">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="c0e30-142">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c0e30-143">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="c0e30-143">The latest Windows 10 SDK</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c0e30-144">Unity 2017.4</span><span class="sxs-lookup"><span data-stu-id="c0e30-144">Unity 2017.4</span></span>](install-the-tools.md#installation-checklist)
- [<span data-ttu-id="c0e30-145">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="c0e30-145">Visual Studio 2017</span></span>](install-the-tools.md#installation-checklist)
- <span data-ttu-id="c0e30-146">Un [casque (VR) immersif de Windows Mixed Reality](immersive-headset-hardware-details.md) ou [Microsoft HoloLens](hololens-hardware-details.md) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="c0e30-146">A [Windows Mixed Reality immersive (VR) headset](immersive-headset-hardware-details.md) or [Microsoft HoloLens](hololens-hardware-details.md) with Developer mode enabled</span></span>
- <span data-ttu-id="c0e30-147">Un appareil photo connecté à votre PC (pour le développement de casque immersives)</span><span class="sxs-lookup"><span data-stu-id="c0e30-147">A camera connected to your PC (for immersive headset development)</span></span>
- <span data-ttu-id="c0e30-148">Accès à Internet pour le programme d’installation Azure et l’extraction de l’API de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-148">Internet access for Azure setup and Custom Vision API retrieval</span></span>
- <span data-ttu-id="c0e30-149">Une série d’au moins cinq (5) images (dix (10) recommandé) pour chaque objet que vous souhaitez que le Service Vision personnalisée pour reconnaître.</span><span class="sxs-lookup"><span data-stu-id="c0e30-149">A series of at least five (5) images (ten (10) recommended) for each object that you would like the Custom Vision Service to recognize.</span></span> <span data-ttu-id="c0e30-150">Si vous le souhaitez, vous pouvez utiliser [les images déjà fournis avec ce cours (une souris et un clavier) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span><span class="sxs-lookup"><span data-stu-id="c0e30-150">If you wish, you can use [the images already provided with this course (a computer mouse and a keyboard) ](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c0e30-151">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="c0e30-151">Before you start</span></span>

1.  <span data-ttu-id="c0e30-152">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="c0e30-152">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="c0e30-153">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c0e30-153">Set up and test your HoloLens.</span></span> <span data-ttu-id="c0e30-154">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="c0e30-154">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="c0e30-155">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="c0e30-155">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="c0e30-156">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="c0e30-156">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="c0e30-157">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="c0e30-157">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-custom-vision-service-portal"></a><span data-ttu-id="c0e30-158">Chapitre 1 : le portail de Service Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-158">Chapter 1 - The Custom Vision Service Portal</span></span>

<span data-ttu-id="c0e30-159">Pour utiliser le *Service Vision personnalisée* dans Azure, vous devez configurer une instance du Service à être mis à disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="c0e30-159">To use the *Custom Vision Service* in Azure, you will need to configure an instance of the Service to be made available to your application.</span></span>

1.  <span data-ttu-id="c0e30-160">Tout d’abord, [accédez à la *Service Vision personnalisée* page principale](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span><span class="sxs-lookup"><span data-stu-id="c0e30-160">First, [navigate to the *Custom Vision Service* main page](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span></span>

2.  <span data-ttu-id="c0e30-161">Cliquez sur le **prise en main** bouton.</span><span class="sxs-lookup"><span data-stu-id="c0e30-161">Click on the **Get Started** button.</span></span>

    ![](images/AzureLabs-Lab302b-01.png)

3.  <span data-ttu-id="c0e30-162">Se connecter à la *Service Vision personnalisée* portail.</span><span class="sxs-lookup"><span data-stu-id="c0e30-162">Sign in to the *Custom Vision Service* Portal.</span></span>

    ![](images/AzureLabs-Lab302b-02.png)

    > [!NOTE]
    > <span data-ttu-id="c0e30-163">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="c0e30-163">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="c0e30-164">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="c0e30-164">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

4.  <span data-ttu-id="c0e30-165">Une fois que vous êtes connecté pour la première fois, vous serez invité au *termes du contrat de Service* Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="c0e30-165">Once you are logged in for the first time, you will be prompted with the *Terms of Service* panel.</span></span> <span data-ttu-id="c0e30-166">Cliquez sur la case à cocher pour accepter les termes du contrat.</span><span class="sxs-lookup"><span data-stu-id="c0e30-166">Click on the checkbox to agree to the terms.</span></span> <span data-ttu-id="c0e30-167">Cliquez ensuite sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-167">Then click on **I agree**.</span></span>

    ![](images/AzureLabs-Lab302b-03.png)

5.  <span data-ttu-id="c0e30-168">Ayant accepté les termes du contrat, vous serez redirigé vers le *projets* section du portail.</span><span class="sxs-lookup"><span data-stu-id="c0e30-168">Having agreed to the Terms, you will be navigated to the *Projects* section of the Portal.</span></span> <span data-ttu-id="c0e30-169">Cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-169">Click on **New Project**.</span></span>

    ![](images/AzureLabs-Lab302b-04.png)

6.  <span data-ttu-id="c0e30-170">Un onglet s’affiche sur le côté droit, qui vous invite à spécifier des champs pour le projet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-170">A tab will appear on the right-hand side, which will prompt you to specify some fields for the project.</span></span>

    1.  <span data-ttu-id="c0e30-171">Insérer un *nom* pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-171">Insert a *Name* for your project.</span></span>

    2.  <span data-ttu-id="c0e30-172">Insérer un *Description* pour votre projet (*facultatif*).</span><span class="sxs-lookup"><span data-stu-id="c0e30-172">Insert a *Description* for your project (*optional*).</span></span>

    3.  <span data-ttu-id="c0e30-173">Choisissez un *groupe de ressources* ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="c0e30-173">Choose a *Resource Group* or create a new one.</span></span> <span data-ttu-id="c0e30-174">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="c0e30-174">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="c0e30-175">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="c0e30-175">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

    4. <span data-ttu-id="c0e30-176">Définir le *Types de projets* à **Classification**</span><span class="sxs-lookup"><span data-stu-id="c0e30-176">Set the *Project Types* to **Classification**</span></span>
    
    5. <span data-ttu-id="c0e30-177">Définir le *domaines* comme **général**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-177">Set the *Domains* as **General**.</span></span>

        ![](images/AzureLabs-Lab302b-05.png)

        > <span data-ttu-id="c0e30-178">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez [, consultez l’article de groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="c0e30-178">If you wish to read more about Azure Resource Groups, please [visit the resource group article](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

7.  <span data-ttu-id="c0e30-179">Une fois que vous avez terminé, cliquez sur **créer un projet**, vous serez redirigé vers le Service Vision personnalisée, page du projet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-179">Once you are finished, click on **Create project**, you will be redirected to the Custom Vision Service, project page.</span></span>

## <a name="chapter-2---training-your-custom-vision-project"></a><span data-ttu-id="c0e30-180">Chapitre 2 - formation de votre projet de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-180">Chapter 2 - Training your Custom Vision project</span></span>

<span data-ttu-id="c0e30-181">Une fois dans le portail de Vision personnalisée, votre objectif principal est pour l’apprentissage de votre projet pour reconnaître des objets spécifiques dans des images.</span><span class="sxs-lookup"><span data-stu-id="c0e30-181">Once in the Custom Vision portal, your primary objective is to train your project to recognize specific objects in images.</span></span> <span data-ttu-id="c0e30-182">Vous avez besoin d’au moins cinq (5) les images, même si dix (10) est recommandée, pour chaque objet que vous souhaitez que votre application à reconnaître.</span><span class="sxs-lookup"><span data-stu-id="c0e30-182">You need at least five (5) images, though ten (10) is preferred, for each object that you would like your application to recognize.</span></span> <span data-ttu-id="c0e30-183">[Vous pouvez utiliser les images fournies avec ce cours (une souris et un clavier)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span><span class="sxs-lookup"><span data-stu-id="c0e30-183">[You can use the images provided with this course (a computer mouse and a keyboard)](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/ComputerVision_Images.zip).</span></span> 

<span data-ttu-id="c0e30-184">Pour l’apprentissage de votre projet de Service Vision personnalisée :</span><span class="sxs-lookup"><span data-stu-id="c0e30-184">To train your Custom Vision Service project:</span></span>

1.  <span data-ttu-id="c0e30-185">Cliquez sur le **+** situé en regard **balises.**</span><span class="sxs-lookup"><span data-stu-id="c0e30-185">Click on the **+** button next to **Tags.**</span></span>

    ![](images/AzureLabs-Lab302b-06.png)

2.  <span data-ttu-id="c0e30-186">Ajouter le **nom** de l’objet à reconnaître.</span><span class="sxs-lookup"><span data-stu-id="c0e30-186">Add the **name** of the object you would like to recognize.</span></span> <span data-ttu-id="c0e30-187">Cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-187">Click on **Save**.</span></span>

    ![](images/AzureLabs-Lab302b-07.png)

3.  <span data-ttu-id="c0e30-188">Vous remarquerez votre **balise** a été ajouté (vous devrez peut-être recharger votre page pour qu’il apparaisse).</span><span class="sxs-lookup"><span data-stu-id="c0e30-188">You will notice your **Tag** has been added (you may need to reload your page for it to appear).</span></span> <span data-ttu-id="c0e30-189">Cliquez sur la case à cocher à côté de votre nouvelle balise, si elle n’est pas activée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-189">Click the checkbox alongside your new tag, if it is not already checked.</span></span>

    ![](images/AzureLabs-Lab302b-08.png)

4.  <span data-ttu-id="c0e30-190">Cliquez sur **ajouter des Images** dans le centre de la page.</span><span class="sxs-lookup"><span data-stu-id="c0e30-190">Click on **Add Images** in the center of the page.</span></span>

    ![](images/AzureLabs-Lab302b-09.png)

5.  <span data-ttu-id="c0e30-191">Cliquez sur **parcourir les fichiers locaux**, rechercher, puis sélectionnez, les images que vous voulez charger, le minimum étant cinq (5).</span><span class="sxs-lookup"><span data-stu-id="c0e30-191">Click on **Browse local files**, and search, then select, the images you would like to upload, with the minimum being five (5).</span></span> <span data-ttu-id="c0e30-192">N’oubliez pas que toutes ces images doivent contenir l’objet qui sont de formation.</span><span class="sxs-lookup"><span data-stu-id="c0e30-192">Remember all of these images should contain the object which you are training.</span></span>

    > [!NOTE]
    >  <span data-ttu-id="c0e30-193">Vous pouvez sélectionner plusieurs images à la fois, à télécharger.</span><span class="sxs-lookup"><span data-stu-id="c0e30-193">You can select several images at a time, to upload.</span></span>

6.  <span data-ttu-id="c0e30-194">Une fois que vous pouvez afficher les images dans l’onglet, sélectionnez la balise appropriée dans le **Mes balises** boîte.</span><span class="sxs-lookup"><span data-stu-id="c0e30-194">Once you can see the images in the tab, select the appropriate tag in the **My Tags** box.</span></span>

    ![](images/AzureLabs-Lab302b-10.png)

7.  <span data-ttu-id="c0e30-195">Cliquez sur **charger des fichiers**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-195">Click on **Upload files**.</span></span> <span data-ttu-id="c0e30-196">Les fichiers de lancer le chargement.</span><span class="sxs-lookup"><span data-stu-id="c0e30-196">The files will begin uploading.</span></span> <span data-ttu-id="c0e30-197">Une fois que vous avez la confirmation du téléchargement, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-197">Once you have confirmation of the upload, click **Done**.</span></span>

    ![](images/AzureLabs-Lab302b-11.png)

8.  <span data-ttu-id="c0e30-198">Répétez ce processus pour créer un nouveau **balise** nommé **clavier** et télécharger les photos appropriées pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c0e30-198">Repeat the same process to create a new **Tag** named **Keyboard** and upload the appropriate photos for it.</span></span> <span data-ttu-id="c0e30-199">Veillez à **Décochez** *souris* une fois que vous avez créé les nouvelles balises, par conséquent, pour afficher le *ajouter des images* fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c0e30-199">Make sure to **uncheck** *Mouse* once you have created the new tags, so to show the *Add images* window.</span></span>

9.  <span data-ttu-id="c0e30-200">Une fois que vous avez les deux balises à configurer, cliquez sur **Train**, et la première itération d’entraînement commencera la génération.</span><span class="sxs-lookup"><span data-stu-id="c0e30-200">Once you have both Tags set up, click on **Train**, and the first training iteration will start building.</span></span>

    ![](images/AzureLabs-Lab302b-12.png)

10. <span data-ttu-id="c0e30-201">Une fois qu’il est créé, vous serez en mesure de voir les deux boutons nommés **par défaut** et **prédiction URL**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-201">Once it is built, you will be able to see two buttons called **Make default** and **Prediction URL**.</span></span> <span data-ttu-id="c0e30-202">Cliquez sur **par défaut** tout d’abord, puis cliquez sur **prédiction URL**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-202">Click on **Make default** first, then click on **Prediction URL**.</span></span>

    ![](images/AzureLabs-Lab302b-13.png)

    > [!NOTE] 
    > <span data-ttu-id="c0e30-203">L’URL de point de terminaison qui est fourni à partir de ce problème, selon ce qui a *itération* a été marquée comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="c0e30-203">The endpoint URL which is provided from this, is set to whichever *Iteration* has been marked as default.</span></span> <span data-ttu-id="c0e30-204">Par conséquent, si vous apportez ultérieurement un nouveau *itération* et mettez-le à jour comme valeur par défaut, vous ne devez pas modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="c0e30-204">As such, if you later make a new *Iteration* and update it as default, you will not need to change your code.</span></span>

11. <span data-ttu-id="c0e30-205">Une fois que vous avez cliqué sur *prédiction URL*, ouvrez *le bloc-notes*, puis copiez et collez le **URL** et **prédiction-clé**, de sorte que vous pouvez récupérer lorsque vous en avez besoin plus loin dans le code.</span><span class="sxs-lookup"><span data-stu-id="c0e30-205">Once you have clicked on *Prediction URL*, open *Notepad*, and copy and paste the **URL** and the **Prediction-Key**, so that you can retrieve it when you need it later in the code.</span></span>

    ![](images/AzureLabs-Lab302b-14.png)

12. <span data-ttu-id="c0e30-206">Cliquez sur le **représentant une roue dentée** dans la partie supérieure droite de l’écran.</span><span class="sxs-lookup"><span data-stu-id="c0e30-206">Click on the **Cog** at the top right of the screen.</span></span>

    ![](images/AzureLabs-Lab302b-15.png)

13. <span data-ttu-id="c0e30-207">Copie le **formation clé** et collez-la dans un *le bloc-notes*, pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c0e30-207">Copy the **Training Key** and paste it into a *Notepad*, for later use.</span></span>

    ![](images/AzureLabs-Lab302b-16.png)

14. <span data-ttu-id="c0e30-208">Copiez également votre **Id de projet**et également le coller dans votre *le bloc-notes* fichier, pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="c0e30-208">Also copy your **Project Id**, and also paste it into your *Notepad* file, for later use.</span></span>

    ![](images/AzureLabs-Lab302b-16a.png)

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="c0e30-209">Chapitre 3 - configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="c0e30-209">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="c0e30-210">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="c0e30-210">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="c0e30-211">Ouvrez *Unity* et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-211">Open *Unity* and click **New**.</span></span>

    ![](images/AzureLabs-Lab302b-17.png)

2.  <span data-ttu-id="c0e30-212">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-212">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="c0e30-213">Insérer **AzureCustomVision.**</span><span class="sxs-lookup"><span data-stu-id="c0e30-213">Insert **AzureCustomVision.**</span></span> <span data-ttu-id="c0e30-214">Assurez-vous que le modèle de projet est défini sur **3D**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-214">Make sure the project template is set to **3D**.</span></span> <span data-ttu-id="c0e30-215">Définir le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="c0e30-215">Set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="c0e30-216">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-216">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab302b-18.png)

3.  <span data-ttu-id="c0e30-217">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-217">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="c0e30-218">Accédez à **modifier* > *préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-218">Go to **Edit* > *Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="c0e30-219">Modification **éditeur de Script externe** à **Visual Studio 2017**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-219">Change **External Script Editor** to **Visual Studio 2017**.</span></span> <span data-ttu-id="c0e30-220">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="c0e30-220">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab302b-19.png)

4.  <span data-ttu-id="c0e30-221">Ensuite, accédez à **fichier > Paramètres de Build** et sélectionnez **plateforme Windows universelle**, puis cliquez sur le **plateforme de commutation** bouton pour appliquer votre sélection.</span><span class="sxs-lookup"><span data-stu-id="c0e30-221">Next, go to **File > Build Settings** and select **Universal Windows Platform**, then click on the **Switch Platform** button to apply your selection.</span></span>

    ![](images/AzureLabs-Lab302b-20.png)

5.  <span data-ttu-id="c0e30-222">Lorsque vous êtes toujours dans **fichier > Paramètres de Build** et vous assurer que :</span><span class="sxs-lookup"><span data-stu-id="c0e30-222">While still in **File > Build Settings** and make sure that:</span></span>

    1.  <span data-ttu-id="c0e30-223">**Équipement cible** a la valeur **Hololens**</span><span class="sxs-lookup"><span data-stu-id="c0e30-223">**Target Device** is set to **Hololens**</span></span>

        > <span data-ttu-id="c0e30-224">Pour des casques IMMERSIFS, définissez **appareil cible** à *n’importe quel appareil*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-224">For the immersive headsets, set **Target Device** to *Any Device*.</span></span>
        
    2.  <span data-ttu-id="c0e30-225">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="c0e30-225">**Build Type** is set to **D3D**</span></span>
    3.  <span data-ttu-id="c0e30-226">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="c0e30-226">**SDK** is set to **Latest installed**</span></span>
    4.  <span data-ttu-id="c0e30-227">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="c0e30-227">**Visual Studio Version** is set to **Latest installed**</span></span>
    5.  <span data-ttu-id="c0e30-228">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="c0e30-228">**Build and Run** is set to **Local Machine**</span></span>
    6.  <span data-ttu-id="c0e30-229">Enregistrer la scène et l’ajouter à la build.</span><span class="sxs-lookup"><span data-stu-id="c0e30-229">Save the scene and add it to the build.</span></span> 

        1. <span data-ttu-id="c0e30-230">Cela en sélectionnant **ajouter un arrière-plan Open**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-230">Do this by selecting **Add Open Scenes**.</span></span> <span data-ttu-id="c0e30-231">Une fenêtre d’enregistrement s’affiche.</span><span class="sxs-lookup"><span data-stu-id="c0e30-231">A save window will appear.</span></span>

            ![](images/AzureLabs-Lab302b-21.png)

        2. <span data-ttu-id="c0e30-232">Créer un nouveau dossier pour cela et n’importe quel futur, votre scène, puis sélectionnez le **nouveau dossier** bouton permettant de créer un nouveau dossier, nommez-le **scènes**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-232">Create a new folder for this, and any future, scene, then select the **New folder** button, to create a new folder, name it **Scenes**.</span></span>

            ![](images/AzureLabs-Lab302b-22.png)

        3. <span data-ttu-id="c0e30-233">Ouvrez votre nouvellement créé **scènes** dossier, puis, dans le *nom de fichier :* champ de texte, tapez **CustomVisionScene**, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-233">Open your newly created **Scenes** folder, and then in the *File name:* text field, type **CustomVisionScene**, then click on **Save**.</span></span>

            ![](images/AzureLabs-Lab302b-23.png)

            > <span data-ttu-id="c0e30-234">N’oubliez pas, vous devez enregistrer vos séquences de Unity dans le *actifs* dossier, car ils doivent être associées au projet Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-234">Be aware, you must save your Unity scenes within the *Assets* folder, as they must be associated with the Unity project.</span></span> <span data-ttu-id="c0e30-235">Création du dossier de scènes (et autres dossiers similaire) est un moyen classique de structurer un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-235">Creating the scenes folder (and other similar folders) is a typical way of structuring a Unity project.</span></span>
            
    7.  <span data-ttu-id="c0e30-236">Les autres paramètres, dans *paramètres de Build*, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="c0e30-236">The remaining settings, in *Build Settings*, should be left as default for now.</span></span>

        ![](images/AzureLabs-Lab302b-24.png)

6.  <span data-ttu-id="c0e30-237">Dans le *paramètres de Build* fenêtre, cliquez sur le **paramètres du lecteur** bouton, s’ouvre le panneau de configuration connexe dans l’espace où le *inspecteur* se trouve.</span><span class="sxs-lookup"><span data-stu-id="c0e30-237">In the *Build Settings* window, click on the **Player Settings** button, this will open the related panel in the space where the *Inspector* is located.</span></span>

7. <span data-ttu-id="c0e30-238">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="c0e30-238">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="c0e30-239">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="c0e30-239">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="c0e30-240">**Version du Runtime de script** doit être **expérimental (équivalent .NET 4.6)**, ce qui déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-240">**Scripting Runtime Version** should be **Experimental (.NET 4.6 Equivalent)**, which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="c0e30-241">**Script principal** doit être **.NET**</span><span class="sxs-lookup"><span data-stu-id="c0e30-241">**Scripting Backend** should be **.NET**</span></span>

        3. <span data-ttu-id="c0e30-242">**Niveau de compatibilité d’API** doit être **.NET 4.6**</span><span class="sxs-lookup"><span data-stu-id="c0e30-242">**API Compatibility Level** should be **.NET 4.6**</span></span>

        ![](images/AzureLabs-Lab302b-25.png)

    2.  <span data-ttu-id="c0e30-243">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="c0e30-243">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="c0e30-244">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="c0e30-244">**InternetClient**</span></span>

        2.  <span data-ttu-id="c0e30-245">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="c0e30-245">**Webcam**</span></span>

        3. <span data-ttu-id="c0e30-246">**Microphone**</span><span class="sxs-lookup"><span data-stu-id="c0e30-246">**Microphone**</span></span>

        ![](images/AzureLabs-Lab302b-26.png)

    3.  <span data-ttu-id="c0e30-247">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, assurez-vous que le **SDK de réalité mixte Windows**  est ajouté.</span><span class="sxs-lookup"><span data-stu-id="c0e30-247">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, make sure the **Windows Mixed Reality SDK** is added.</span></span>

    ![](images/AzureLabs-Lab302b-27.png)

8.  <span data-ttu-id="c0e30-248">Dans *paramètres de Build* *Unity C\# projets* est n’est plus grisée ; Cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="c0e30-248">Back in *Build Settings* *Unity C\# Projects* is no longer greyed out; tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="c0e30-249">Fermez la fenêtre Paramètres de Build.</span><span class="sxs-lookup"><span data-stu-id="c0e30-249">Close the Build Settings window.</span></span>

10.  <span data-ttu-id="c0e30-250">Enregistrer votre projet et la scène (**fichier > Enregistrer la scène / fichier > Enregistrer le projet**).</span><span class="sxs-lookup"><span data-stu-id="c0e30-250">Save your Scene and project (**FILE > SAVE SCENE / FILE > SAVE PROJECT**).</span></span>


## <a name="chapter-4---importing-the-newtonsoft-dll-in-unity"></a><span data-ttu-id="c0e30-251">Chapitre 4 - Importation de la DLL Newtonsoft dans Unity</span><span class="sxs-lookup"><span data-stu-id="c0e30-251">Chapter 4 - Importing the Newtonsoft DLL in Unity</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0e30-252">Si vous souhaitez ignorer la *Unity configurer* composant de ce cours et continuer directement dans le code, n’hésitez pas à télécharger ce [Azure-MR-302b.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), importez-le dans votre projet en tant qu’un [ **Package personnalisé**](https://docs.unity3d.com/Manual/AssetPackages.html), puis continuez à partir de [chapitre 6](#chapter-6---create-the-customvisionanalyser-class).</span><span class="sxs-lookup"><span data-stu-id="c0e30-252">If you wish to skip the *Unity Set up* component of this course, and continue straight into code, feel free to download this [Azure-MR-302b.unitypackage](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/Azure-MR-302b.unitypackage), import it into your project as a [**Custom Package**](https://docs.unity3d.com/Manual/AssetPackages.html), and then continue from [Chapter 6](#chapter-6---create-the-customvisionanalyser-class).</span></span>

<span data-ttu-id="c0e30-253">Ce cours nécessite l’utilisation de la **Newtonsoft** bibliothèque que vous pouvez ajouter en tant que DLL à vos ressources.</span><span class="sxs-lookup"><span data-stu-id="c0e30-253">This course requires the use of the **Newtonsoft** library, which you can add as a DLL to your assets.</span></span> <span data-ttu-id="c0e30-254">Le package contenant [cette bibliothèque peut être téléchargée à partir de ce lien](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="c0e30-254">The package containing [this library can be downloaded from this Link](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20302b%20-%20Custom%20vision/NewtonsoftDLL.unitypackage).</span></span>
<span data-ttu-id="c0e30-255">Pour importer la bibliothèque Newtonsoft dans votre projet, utilisez le Package Unity qui accompagne ce cours.</span><span class="sxs-lookup"><span data-stu-id="c0e30-255">To import the Newtonsoft library into your project, use the Unity Package which came with this course.</span></span>

1.  <span data-ttu-id="c0e30-256">Ajouter le *.unitypackage* à Unity à l’aide de la **actifs* > *importation* *Package*  >  *Personnalisé* *Package** option de menu.</span><span class="sxs-lookup"><span data-stu-id="c0e30-256">Add the *.unitypackage* to Unity by using the **Assets* > *Import* *Package* > *Custom* *Package** menu option.</span></span>

2.  <span data-ttu-id="c0e30-257">Dans le **importer un Package Unity** emballer qui apparaît, vérifiez tous les éléments sous (y compris) **plug-ins** est sélectionné.</span><span class="sxs-lookup"><span data-stu-id="c0e30-257">In the **Import Unity Package** box that pops up, ensure everything under (and including) **Plugins** is selected.</span></span>

    ![](images/AzureLabs-Lab302b-28.png)

3.  <span data-ttu-id="c0e30-258">Cliquez sur le **importation** pour ajouter les éléments à votre projet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-258">Click the **Import** button to add the items to your project.</span></span>

4.  <span data-ttu-id="c0e30-259">Accédez à la **Newtonsoft** dossier sous **plug-ins** dans la vue du projet, puis sélectionnez le *plug-in de Newtonsoft.Json*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-259">Go to the **Newtonsoft** folder under **Plugins** in the project view and select the *Newtonsoft.Json plugin*.</span></span>

    ![](images/AzureLabs-Lab302b-29.png)

5.  <span data-ttu-id="c0e30-260">Avec le *plug-in de Newtonsoft.Json* sélectionnée, vérifiez que **plateforme Any** est **unchecked**, puis assurez-vous que **WSAPlayer** est également **unchecked**, puis cliquez sur **appliquer**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-260">With the *Newtonsoft.Json plugin* selected, ensure that **Any Platform** is **unchecked**, then ensure that **WSAPlayer** is also **unchecked**, then click **Apply**.</span></span> <span data-ttu-id="c0e30-261">Il s’agit juste pour confirmer que les fichiers sont correctement configurés.</span><span class="sxs-lookup"><span data-stu-id="c0e30-261">This is just to confirm that the files are configured correctly.</span></span>

    ![](images/AzureLabs-Lab302b-30.png)

    > [!NOTE]
    > <span data-ttu-id="c0e30-262">Marquage de ces plug-ins les configure uniquement à être utilisé dans l’éditeur Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-262">Marking these plugins configures them to only be used in the Unity Editor.</span></span> <span data-ttu-id="c0e30-263">Il existe un ensemble différent d’eux dans le dossier WSA qui sera utilisé une fois que le projet est exporté à partir d’Unity.</span><span class="sxs-lookup"><span data-stu-id="c0e30-263">There are a different set of them in the WSA folder which will be used after the project is exported from Unity.</span></span>

6.  <span data-ttu-id="c0e30-264">Ensuite, vous devez ouvrir le **WSA** dossier, en respectant le **Newtonsoft** dossier.</span><span class="sxs-lookup"><span data-stu-id="c0e30-264">Next, you need to open the **WSA** folder, within the **Newtonsoft** folder.</span></span> <span data-ttu-id="c0e30-265">Vous verrez une copie du même fichier que vous venez de configurer.</span><span class="sxs-lookup"><span data-stu-id="c0e30-265">You will see a copy of the same file you just configured.</span></span> <span data-ttu-id="c0e30-266">Sélectionnez le fichier et dans l’inspecteur, vérifiez que</span><span class="sxs-lookup"><span data-stu-id="c0e30-266">Select the file, and then in the inspector, ensure that</span></span>
    -   <span data-ttu-id="c0e30-267">**N’importe quelle plateforme** est **non contrôlé**</span><span class="sxs-lookup"><span data-stu-id="c0e30-267">**Any Platform** is **unchecked**</span></span> 
    -   <span data-ttu-id="c0e30-268">**uniquement** **WSAPlayer** est **activée**</span><span class="sxs-lookup"><span data-stu-id="c0e30-268">**only** **WSAPlayer** is **checked**</span></span>
    -   <span data-ttu-id="c0e30-269">**Ne pas traiter les** est **activée**</span><span class="sxs-lookup"><span data-stu-id="c0e30-269">**Dont process** is **checked**</span></span>

    ![](images/AzureLabs-Lab302b-31.png)

## <a name="chapter-5---camera-setup"></a><span data-ttu-id="c0e30-270">Chapitre 5 - installation de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="c0e30-270">Chapter 5 - Camera setup</span></span>

1.  <span data-ttu-id="c0e30-271">Dans le volet de la hiérarchie, sélectionnez le *Main Camera*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-271">In the Hierarchy Panel, select the *Main Camera*.</span></span>

2.  <span data-ttu-id="c0e30-272">Une fois sélectionné, vous serez en mesure de voir tous les composants de la *Main Camera* dans le *panneau Inspecteur*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-272">Once selected, you will be able to see all the components of the *Main Camera* in the *Inspector Panel*.</span></span>

    1.  <span data-ttu-id="c0e30-273">Le *caméra* objet doit être nommé **Main Camera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="c0e30-273">The *camera* object must be named **Main Camera** (note the spelling!)</span></span>

    2.  <span data-ttu-id="c0e30-274">La caméra principale **balise** doit être définie sur **MainCamera** (Notez l’orthographe !)</span><span class="sxs-lookup"><span data-stu-id="c0e30-274">The Main Camera **Tag** must be set to **MainCamera** (note the spelling!)</span></span>

    3.  <span data-ttu-id="c0e30-275">Assurez-vous que le **Position transformer** a la valeur **0, 0, 0**</span><span class="sxs-lookup"><span data-stu-id="c0e30-275">Make sure the **Transform Position** is set to **0, 0, 0**</span></span>

    4.  <span data-ttu-id="c0e30-276">Définissez **effacer les indicateurs** à **couleur unie** (ignorer cela pour casque immersif).</span><span class="sxs-lookup"><span data-stu-id="c0e30-276">Set **Clear Flags** to **Solid Color** (ignore this for immersive headset).</span></span>

    5.  <span data-ttu-id="c0e30-277">Définir le **arrière-plan** couleur de l’appareil photo à **noir, Alpha 0 (Hex Code : #00000000)** (ignorer cela pour casque immersif).</span><span class="sxs-lookup"><span data-stu-id="c0e30-277">Set the **Background** Color of the camera Component to **Black, Alpha 0 (Hex Code: #00000000)** (ignore this for immersive headset).</span></span>

    ![](images/AzureLabs-Lab302b-32.png)


## <a name="chapter-6---create-the-customvisionanalyser-class"></a><span data-ttu-id="c0e30-278">Chapitre 6 : créer la classe CustomVisionAnalyser.</span><span class="sxs-lookup"><span data-stu-id="c0e30-278">Chapter 6 - Create the CustomVisionAnalyser class.</span></span>

<span data-ttu-id="c0e30-279">À ce stade, vous êtes prêt à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="c0e30-279">At this point you are ready to write some code.</span></span>

<span data-ttu-id="c0e30-280">Vous allez commencer avec le *CustomVisionAnalyser* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-280">You will begin with the *CustomVisionAnalyser* class.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e30-281">Les appels à la **Service Vision personnalisée** apportées dans le code indiqué ci-dessous sont établies en utilisant le **API REST de Vision personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-281">The calls to the **Custom Vision Service** made in the code shown below are made using the **Custom Vision REST API**.</span></span> <span data-ttu-id="c0e30-282">Via l’utilisant, vous verrez comment implémenter et utiliser cette API (utile pour comprendre comment implémenter quelque chose de similaire sur votre propre).</span><span class="sxs-lookup"><span data-stu-id="c0e30-282">Through using this, you will see how to implement and make use of this API (useful for understanding how to implement something similar on your own).</span></span> <span data-ttu-id="c0e30-283">Sachez que Microsoft propose un **Custom Vision Service SDK** qui peut également être utilisé pour effectuer des appels au Service.</span><span class="sxs-lookup"><span data-stu-id="c0e30-283">Be aware, that Microsoft offers a **Custom Vision Service SDK** that can also be used to make calls to the Service.</span></span> <span data-ttu-id="c0e30-284">Pour plus d’informations, visitez le [Custom Vision Service SDK](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) article.</span><span class="sxs-lookup"><span data-stu-id="c0e30-284">For more information visit the [Custom Vision Service SDK](https://github.com/Microsoft/Cognitive-CustomVision-Windows/) article.</span></span>

<span data-ttu-id="c0e30-285">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="c0e30-285">This class is responsible for:</span></span>

-   <span data-ttu-id="c0e30-286">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="c0e30-286">Loading the latest image captured as an array of bytes.</span></span>

-   <span data-ttu-id="c0e30-287">Envoyer le tableau d’octets à votre Azure *Service Vision personnalisée* instance pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="c0e30-287">Sending the byte array to your Azure *Custom Vision Service* instance for analysis.</span></span>

-   <span data-ttu-id="c0e30-288">Recevoir une réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="c0e30-288">Receiving the response as a JSON string.</span></span>

-   <span data-ttu-id="c0e30-289">La désérialisation de la réponse et en passant résultant *prédiction* à la *SceneOrganiser* (classe), qui se chargera de la façon dont la réponse doit être affichée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-289">Deserializing the response and passing the resulting *Prediction* to the *SceneOrganiser* class, which will take care of how the response should be displayed.</span></span>

<span data-ttu-id="c0e30-290">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-290">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-291">Avec le bouton droit dans le *dossier composants* situé dans le *panneau projet*, puis cliquez sur **créer > dossier**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-291">Right-click in the *Asset Folder* located in the *Project Panel*, then click **Create > Folder**.</span></span> <span data-ttu-id="c0e30-292">Appelez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-292">Call the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab302b-33.png)

2.  <span data-ttu-id="c0e30-293">Double-cliquez sur le dossier venez de créer, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c0e30-293">Double-click on the folder just created, to open it.</span></span>

3.  <span data-ttu-id="c0e30-294">Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-294">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="c0e30-295">Nommez le script *CustomVisionAnalyser*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-295">Name the script *CustomVisionAnalyser*.</span></span>

4.  <span data-ttu-id="c0e30-296">Double-cliquez sur le nouveau *CustomVisionAnalyser* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-296">Double-click on the new *CustomVisionAnalyser* script to open it with **Visual Studio**.</span></span>

5.  <span data-ttu-id="c0e30-297">Mettre à jour les espaces de noms en haut de votre fichier pour correspondre à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="c0e30-297">Update the namespaces at the top of your file to match the following:</span></span>

    ```csharp
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    using Newtonsoft.Json;
    ```

6.  <span data-ttu-id="c0e30-298">Dans le *CustomVisionAnalyser* de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0e30-298">In the *CustomVisionAnalyser* class, add the following variables:</span></span>

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
    > <span data-ttu-id="c0e30-299">Assurez-vous que vous insérez votre **prédiction clé** dans le **predictionKey** variable et votre **point de terminaison de prédiction** dans le **predictionEndpoint** variable.</span><span class="sxs-lookup"><span data-stu-id="c0e30-299">Make sure you insert your **Prediction Key** into the **predictionKey** variable and your **Prediction Endpoint** into the **predictionEndpoint** variable.</span></span> <span data-ttu-id="c0e30-300">Vous avez copié à *le bloc-notes* plus haut dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="c0e30-300">You copied these to *Notepad* earlier in the course.</span></span>

7.  <span data-ttu-id="c0e30-301">Code pour **Awake()** doit maintenant être ajouté pour initialiser la variable d’Instance :</span><span class="sxs-lookup"><span data-stu-id="c0e30-301">Code for **Awake()** now needs to be added to initialize the Instance variable:</span></span>

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

8.  <span data-ttu-id="c0e30-302">Supprimez les méthodes **Start()** et **Update()**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-302">Delete the methods **Start()** and **Update()**.</span></span>

9.  <span data-ttu-id="c0e30-303">Ensuite, ajoutez la coroutine (avec la méthode statique **GetImageAsByteArray()** méthode en dessous), qui obtient les résultats de l’analyse de l’image capturée par le *ImageCapture* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-303">Next, add the coroutine (with the static **GetImageAsByteArray()** method below it), which will obtain the results of the analysis of the image captured by the *ImageCapture* class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="c0e30-304">Dans le **AnalyseImageCapture** coroutine, il existe un appel à la *SceneOrganiser* classe que vous êtes encore à créer.</span><span class="sxs-lookup"><span data-stu-id="c0e30-304">In the **AnalyseImageCapture** coroutine, there is a call to the *SceneOrganiser* class that you are yet to create.</span></span> <span data-ttu-id="c0e30-305">Par conséquent, **laisser les lignes commentées pour l’instant**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-305">Therefore, **leave those lines commented for now**.</span></span>

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

10.  <span data-ttu-id="c0e30-306">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-306">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

## <a name="chapter-7---create-the-customvisionobjects-class"></a><span data-ttu-id="c0e30-307">Chapitre 7 - créer la classe CustomVisionObjects</span><span class="sxs-lookup"><span data-stu-id="c0e30-307">Chapter 7 - Create the CustomVisionObjects class</span></span>

<span data-ttu-id="c0e30-308">La classe que vous allez créer est maintenant le *CustomVisionObjects* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-308">The class you will create now is the *CustomVisionObjects* class.</span></span>

<span data-ttu-id="c0e30-309">Ce script contient un nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels effectués à la *Service Vision personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-309">This script contains a number of objects used by other classes to serialize and deserialize the calls made to the *Custom Vision Service*.</span></span>

> [!WARNING]
> <span data-ttu-id="c0e30-310">Il est important que vous notez le point de terminaison du Service de Vision personnalisé vous fournit, comme le JSON ci-dessous, structure a été configurée pour fonctionner avec [ *v2.0 de prédiction de Vision personnalisée*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290).</span><span class="sxs-lookup"><span data-stu-id="c0e30-310">It is important that you take note of the endpoint that the Custom Vision Service provides you, as the below JSON structure has been set up to work with [*Custom Vision Prediction v2.0*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/450e4ba4d72542e889d93fd7b8e960de/operations/5a6264bc40d86a0ef8b2c290).</span></span> <span data-ttu-id="c0e30-311">Si vous avez une version différente, vous devrez peut-être mettre à jour le ci-dessous structure.</span><span class="sxs-lookup"><span data-stu-id="c0e30-311">If you have a different version, you may need to update the below structure.</span></span>

<span data-ttu-id="c0e30-312">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-312">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-313">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-313">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="c0e30-314">Appeler le script *CustomVisionObjects*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-314">Call the script *CustomVisionObjects*.</span></span>

2.  <span data-ttu-id="c0e30-315">Double-cliquez sur le nouveau **CustomVisionObjects** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-315">Double-click on the new **CustomVisionObjects** script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="c0e30-316">Ajoutez les espaces de noms suivantes au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="c0e30-316">Add the following namespaces to the top of the file:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="c0e30-317">Supprimer le **Start()** et **Update()** méthodes à l’intérieur de la *CustomVisionObjects* classe ; cette classe doit maintenant être vide.</span><span class="sxs-lookup"><span data-stu-id="c0e30-317">Delete the **Start()** and **Update()** methods inside the *CustomVisionObjects* class; this class should now be empty.</span></span>

5.  <span data-ttu-id="c0e30-318">Ajoutez les classes suivantes **en dehors de** le *CustomVisionObjects* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-318">Add the following classes **outside** the *CustomVisionObjects* class.</span></span> <span data-ttu-id="c0e30-319">Ces objets sont utilisés par le *Newtonsoft* bibliothèque pour sérialiser et désérialiser les données de réponse :</span><span class="sxs-lookup"><span data-stu-id="c0e30-319">These objects are used by the *Newtonsoft* library to serialize and deserialize the response data:</span></span>

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

## <a name="chapter-8---create-the-voicerecognizer-class"></a><span data-ttu-id="c0e30-320">Chapitre 8 - créer la classe VoiceRecognizer</span><span class="sxs-lookup"><span data-stu-id="c0e30-320">Chapter 8 - Create the VoiceRecognizer class</span></span>

<span data-ttu-id="c0e30-321">Cette classe reconnaîtra l’entrée vocale à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-321">This class will recognize the voice input from the user.</span></span>

<span data-ttu-id="c0e30-322">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-322">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-323">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-323">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="c0e30-324">Appeler le script *VoiceRecognizer*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-324">Call the script *VoiceRecognizer*.</span></span>

2.  <span data-ttu-id="c0e30-325">Double-cliquez sur le nouveau **VoiceRecognizer** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-325">Double-click on the new **VoiceRecognizer** script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="c0e30-326">Ajouter des espaces de noms suivants ci-dessus le *VoiceRecognizer* classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-326">Add the following namespaces above the *VoiceRecognizer* class:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.Windows.Speech;
    ```

4.  <span data-ttu-id="c0e30-327">Puis ajoutez les variables suivantes à l’intérieur de la *VoiceRecognizer* classe ci-dessus le *Start()* méthode :</span><span class="sxs-lookup"><span data-stu-id="c0e30-327">Then add the following variables inside the *VoiceRecognizer* class, above the *Start()* method:</span></span>

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

5.  <span data-ttu-id="c0e30-328">Ajouter le **Awake()** et **Start()** méthodes, ce dernier qui configureront l’utilisateur *mots clés* pour être reconnus lors de l’association d’une balise à une image :</span><span class="sxs-lookup"><span data-stu-id="c0e30-328">Add the **Awake()** and **Start()** methods, the latter of which will set up the user *keywords* to be recognized when associating a tag to an image:</span></span>

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

6.  <span data-ttu-id="c0e30-329">Supprimer le **Update()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-329">Delete the **Update()** method.</span></span>

7.  <span data-ttu-id="c0e30-330">Ajoutez le gestionnaire suivant, qui est appelé chaque fois que l’entrée vocale est reconnue :</span><span class="sxs-lookup"><span data-stu-id="c0e30-330">Add the following handler, which is called whenever voice input is recognized:</span></span>

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

8.  <span data-ttu-id="c0e30-331">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-331">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

> [!NOTE]
> <span data-ttu-id="c0e30-332">Ne vous inquiétez pas sur le code qui peut sembler avoir une erreur, comme vous fournit des classes de supplémentaires bientôt, ce qui résoudra ces.</span><span class="sxs-lookup"><span data-stu-id="c0e30-332">Do not worry about code which might appear to have an error, as you will provide further classes soon, which will fix these.</span></span>

## <a name="chapter-9---create-the-customvisiontrainer-class"></a><span data-ttu-id="c0e30-333">Chapitre 9 - créer la classe CustomVisionTrainer</span><span class="sxs-lookup"><span data-stu-id="c0e30-333">Chapter 9 - Create the CustomVisionTrainer class</span></span>

<span data-ttu-id="c0e30-334">Cette classe sera chaîner une série d’appels de web pour former le *Service Vision personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-334">This class will chain a series of web calls to train the *Custom Vision Service*.</span></span> <span data-ttu-id="c0e30-335">Chaque appel est expliquée en détail juste au-dessus du code.</span><span class="sxs-lookup"><span data-stu-id="c0e30-335">Each call will be explained in detail right above the code.</span></span>

<span data-ttu-id="c0e30-336">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-336">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-337">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-337">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="c0e30-338">Appeler le script *CustomVisionTrainer*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-338">Call the script *CustomVisionTrainer*.</span></span>

2.  <span data-ttu-id="c0e30-339">Double-cliquez sur le nouveau *CustomVisionTrainer* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-339">Double-click on the new *CustomVisionTrainer* script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="c0e30-340">Ajouter des espaces de noms suivants ci-dessus le *CustomVisionTrainer* classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-340">Add the following namespaces above the *CustomVisionTrainer* class:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.Collections.Generic;
    using System.IO;
    using System.Text;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="c0e30-341">Puis ajoutez les variables suivantes à l’intérieur de la *CustomVisionTrainer* de classe, au-dessus du **Start()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-341">Then add the following variables inside the *CustomVisionTrainer* class, above the **Start()** method.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c0e30-342">L’URL de formation utilisée ici est fourni dans le *1.2 de formation Vision personnalisée* documentation, et a une structure de : https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/</span><span class="sxs-lookup"><span data-stu-id="c0e30-342">The training URL used here is provided within the *Custom Vision Training 1.2* documentation, and has a structure of: https://southcentralus.api.cognitive.microsoft.com/customvision/v1.2/Training/projects/{projectId}/</span></span>  
    > <span data-ttu-id="c0e30-343">Pour plus d’informations, visitez le [ *API de référence de formation de Vision personnalisée v1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span><span class="sxs-lookup"><span data-stu-id="c0e30-343">For more information, visit the [*Custom Vision Training v1.2 reference API*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span></span>

    > [!WARNING]
    > <span data-ttu-id="c0e30-344">Il est important que vous notez le point de terminaison que le Service Vision personnalisée vous fournit pour le mode d’apprentissage, comme la structure JSON utilisée (dans le **CustomVisionObjects** classe) a été configuré pour fonctionner avec [  *Custom Vision v1.2 de formation*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span><span class="sxs-lookup"><span data-stu-id="c0e30-344">It is important that you take note of the endpoint that the Custom Vision Service provides you for the training mode, as the JSON structure used (within the **CustomVisionObjects** class) has been set up to work with [*Custom Vision Training v1.2*](https://southcentralus.dev.cognitive.microsoft.com/docs/services/f2d62aa3b93843d79e948fe87fa89554/operations/5a3044ee08fa5e06b890f11f).</span></span> <span data-ttu-id="c0e30-345">Si vous avez une version différente, vous devrez peut-être mettre à jour le *objets* structure.</span><span class="sxs-lookup"><span data-stu-id="c0e30-345">If you have a different version, you may need to update the *Objects* structure.</span></span>

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
    > <span data-ttu-id="c0e30-346">Veillez à ajouter votre **clé Service** (clé de formation) valeur et **Id de projet** valeur, ce qui vous avez notée précédent ; ce sont les valeurs vous [collectées à partir du portail précédemment dans le (cours Chapitre 2, l’étape 10 et versions ultérieures)](#chapter-2---training-your-custom-vision-oroject).</span><span class="sxs-lookup"><span data-stu-id="c0e30-346">Ensure that you add your **Service Key** (Training Key) value and **Project Id** value, which you noted down previous; these are the values you [collected from the portal earlier in the course (Chapter 2, step 10 onwards)](#chapter-2---training-your-custom-vision-oroject).</span></span>

5.  <span data-ttu-id="c0e30-347">Ajoutez le code suivant **Start()** et **Awake()** méthodes.</span><span class="sxs-lookup"><span data-stu-id="c0e30-347">Add the following **Start()** and **Awake()** methods.</span></span> <span data-ttu-id="c0e30-348">Ces méthodes sont appelées lors de l’initialisation et contient l’appel pour définir l’interface utilisateur :</span><span class="sxs-lookup"><span data-stu-id="c0e30-348">Those methods are called on initialization and contain the call to set up the UI:</span></span>

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

6.  <span data-ttu-id="c0e30-349">Supprimer le **Update()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-349">Delete the **Update()** method.</span></span> <span data-ttu-id="c0e30-350">Cette classe en n'aurez pas besoin.</span><span class="sxs-lookup"><span data-stu-id="c0e30-350">This class will not need it.</span></span>

7.  <span data-ttu-id="c0e30-351">Ajouter le **RequestTagSelection()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-351">Add the **RequestTagSelection()** method.</span></span> <span data-ttu-id="c0e30-352">Cette méthode est le premier à être appelée lorsqu’une image a été capturée et stockée dans l’appareil et est maintenant prêt à être soumis à la *Service Vision personnalisée*, former celui-ci.</span><span class="sxs-lookup"><span data-stu-id="c0e30-352">This method is the first to be called when an image has been captured and stored in the device and is now ready to be submitted to the *Custom Vision Service*, to train it.</span></span> <span data-ttu-id="c0e30-353">Cette méthode s’affiche dans la formation, l’interface utilisateur, un ensemble de mots clés de que l’utilisateur peut utiliser pour baliser l’image qui a été capturée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-353">This method displays, in the training UI, a set of keywords the user can use to tag the image that has been captured.</span></span> <span data-ttu-id="c0e30-354">Il avertit également le *VoiceRecognizer* classe pour commencer à écouter entrée vocale à l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-354">It also alerts the *VoiceRecognizer* class to begin listening to the user for voice input.</span></span>

    ```csharp
        internal void RequestTagSelection()
        {
            trainingUI_TextMesh.gameObject.SetActive(true);
            trainingUI_TextMesh.text = $" \nUse voice command \nto choose between the following tags: \nMouse\nKeyboard \nor say Discard";

            VoiceRecognizer.Instance.keywordRecognizer.Start();
        }
    ```

8.  <span data-ttu-id="c0e30-355">Ajouter le **VerifyTag()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-355">Add the **VerifyTag()** method.</span></span> <span data-ttu-id="c0e30-356">Cette méthode reçoit l’entrée vocale reconnue par le **VoiceRecognizer** classe et vérifier sa validité et commencez le processus d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="c0e30-356">This method will receive the voice input recognized by the **VoiceRecognizer** class and verify its validity, and then begin the training process.</span></span>

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

9.  <span data-ttu-id="c0e30-357">Ajouter le **SubmitImageForTraining()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-357">Add the **SubmitImageForTraining()** method.</span></span> <span data-ttu-id="c0e30-358">Cette méthode commence le processus d’apprentissage Service Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-358">This method will begin the Custom Vision Service training process.</span></span> <span data-ttu-id="c0e30-359">La première étape consiste à récupérer le **Id de la balise** à partir du Service qui est associé à l’entrée vocale validé à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-359">The first step is to retrieve the **Tag Id** from the Service which is associated with the validated speech input from the user.</span></span> <span data-ttu-id="c0e30-360">Le **Id de la balise** puis seront téléchargées, ainsi que l’image.</span><span class="sxs-lookup"><span data-stu-id="c0e30-360">The **Tag Id** will then be uploaded along with the image.</span></span>

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

10. <span data-ttu-id="c0e30-361">Ajouter le **TrainCustomVisionProject()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-361">Add the **TrainCustomVisionProject()** method.</span></span> <span data-ttu-id="c0e30-362">Une fois que l’image a été soumise et marqué, cette méthode est appelée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-362">Once the image has been submitted and tagged, this method will be called.</span></span> <span data-ttu-id="c0e30-363">Il crée une nouvelle itération sera formée avec toutes les images précédentes soumis pour le Service ainsi que l’image venez de télécharger.</span><span class="sxs-lookup"><span data-stu-id="c0e30-363">It will create a new Iteration that will be trained with all the previous images submitted to the Service plus the image just uploaded.</span></span> <span data-ttu-id="c0e30-364">Une fois la formation terminée, cette méthode appelle une méthode pour définir le nouvellement créé **itération** comme **par défaut**, de sorte que le point de terminaison que vous utilisez pour l’analyse est la dernière itération formée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-364">Once the training has been completed, this method will call a method to set the newly created **Iteration** as **Default**, so that the endpoint you are using for analysis is the latest trained iteration.</span></span>

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

11. <span data-ttu-id="c0e30-365">Ajouter le **SetDefaultIteration()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-365">Add the **SetDefaultIteration()** method.</span></span> <span data-ttu-id="c0e30-366">Cette méthode définit l’itération précédemment créée et formée en tant que *par défaut*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-366">This method will set the previously created and trained iteration as *Default*.</span></span> <span data-ttu-id="c0e30-367">Une fois terminé, cette méthode sera obligé de supprimer l’itération précédente existant dans le Service.</span><span class="sxs-lookup"><span data-stu-id="c0e30-367">Once completed, this method will have to delete the previous iteration existing in the Service.</span></span> <span data-ttu-id="c0e30-368">Au moment de la rédaction de ce cours, il existe une limite d’un itérations dix (10) maximal autorisé d’exister en même temps dans le Service.</span><span class="sxs-lookup"><span data-stu-id="c0e30-368">At the time of writing this course, there is a limit of a maximum ten (10) iterations allowed to exist at the same time in the Service.</span></span>

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

12. <span data-ttu-id="c0e30-369">Ajouter le **DeletePreviousIteration()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="c0e30-369">Add the **DeletePreviousIteration()** method.</span></span> <span data-ttu-id="c0e30-370">Cette méthode sera rechercher et supprimer l’itération par défaut précédente :</span><span class="sxs-lookup"><span data-stu-id="c0e30-370">This method will find and delete the previous non-default iteration:</span></span>

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

13. <span data-ttu-id="c0e30-371">La dernière méthode pour ajouter dans cette classe est la **GetImageAsByteArray()** méthode, permet de convertir l’image capturée dans un tableau d’octets sur les appels web.</span><span class="sxs-lookup"><span data-stu-id="c0e30-371">The last method to add in this class is the **GetImageAsByteArray()** method, used on the web calls to convert the image captured into a byte array.</span></span>

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

14. <span data-ttu-id="c0e30-372">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-372">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

## <a name="chapter-10---create-the-sceneorganiser-class"></a><span data-ttu-id="c0e30-373">Chapitre 10 - créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="c0e30-373">Chapter 10 - Create the SceneOrganiser class</span></span>

<span data-ttu-id="c0e30-374">Cette classe sera :</span><span class="sxs-lookup"><span data-stu-id="c0e30-374">This class will:</span></span>

-   <span data-ttu-id="c0e30-375">Créer un **curseur** objet à attacher à la caméra principale.</span><span class="sxs-lookup"><span data-stu-id="c0e30-375">Create a **Cursor** object to attach to the Main Camera.</span></span>

-   <span data-ttu-id="c0e30-376">Créer un **étiquette** objet qui s’affiche lorsque le Service reconnaît les objets du monde réel.</span><span class="sxs-lookup"><span data-stu-id="c0e30-376">Create a **Label** object that will appear when the Service recognizes the real-world objects.</span></span>

-   <span data-ttu-id="c0e30-377">Configurer la caméra principale en joignant les composants appropriés à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="c0e30-377">Set up the Main Camera by attaching the appropriate components to it.</span></span>

-   <span data-ttu-id="c0e30-378">En **Mode Analysis**, générer les étiquettes lors de l’exécution, dans l’espace de monde appropriée par rapport à la position de la caméra principale et afficher les données reçues à partir du Service de Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-378">When in **Analysis Mode**, spawn the Labels at runtime, in the appropriate world space relative to the position of the Main Camera, and display the data received from the Custom Vision Service.</span></span>

-   <span data-ttu-id="c0e30-379">En **Mode d’apprentissage**, générer l’interface utilisateur qui affiche les différentes étapes du processus de formation.</span><span class="sxs-lookup"><span data-stu-id="c0e30-379">When in **Training Mode**, spawn the UI that will display the different stages of the training process.</span></span>

<span data-ttu-id="c0e30-380">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-380">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-381">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-381">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="c0e30-382">Nommez le script *SceneOrganiser*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-382">Name the script *SceneOrganiser*.</span></span>

2.  <span data-ttu-id="c0e30-383">Double-cliquez sur le nouveau *SceneOrganiser* script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-383">Double-click on the new *SceneOrganiser* script to open it with **Visual Studio**.</span></span>

3.  <span data-ttu-id="c0e30-384">Vous devez uniquement un espace de noms, supprimez les autres ci-dessus le *SceneOrganiser* classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-384">You will only need one namespace, remove the others from above the *SceneOrganiser* class:</span></span>

    ```csharp
    using UnityEngine;
    ```

4.  <span data-ttu-id="c0e30-385">Puis ajoutez les variables suivantes à l’intérieur de la *SceneOrganiser* classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="c0e30-385">Then add the following variables inside the *SceneOrganiser* class, above the **Start()** method:</span></span>

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

5.  <span data-ttu-id="c0e30-386">Supprimer le **Start()** et **Update()** méthodes.</span><span class="sxs-lookup"><span data-stu-id="c0e30-386">Delete the **Start()** and **Update()** methods.</span></span>

6.  <span data-ttu-id="c0e30-387">Directement sous les variables, ajoutez le **Awake()** (méthode), qui initialisent la classe et configurer la scène.</span><span class="sxs-lookup"><span data-stu-id="c0e30-387">Right underneath the variables, add the **Awake()** method, which will initialize the class and set up the scene.</span></span>

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

7.  <span data-ttu-id="c0e30-388">À présent ajouter le **CreateCameraCursor()** méthode qui crée et place le curseur Main Camera, et le **CreateLabel()** (méthode), ce qui crée le **libellé d’analyse** objet .</span><span class="sxs-lookup"><span data-stu-id="c0e30-388">Now add the **CreateCameraCursor()** method that creates and positions the Main Camera cursor, and the **CreateLabel()** method, which creates the **Analysis Label** object.</span></span>

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

8. <span data-ttu-id="c0e30-389">Ajouter le **SetCameraStatus()** méthode qui gérera les messages destinés à la maille de texte en fournissant l’état de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="c0e30-389">Add the **SetCameraStatus()** method, which will handle messages intended for the text mesh providing the status of the camera.</span></span>

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

9. <span data-ttu-id="c0e30-390">Ajouter le **PlaceAnalysisLabel()** et **SetTagsToLastLabel()** méthodes, ce qui permettra de générer dynamiquement et afficher les données à partir du Service de Vision personnalisée dans la scène.</span><span class="sxs-lookup"><span data-stu-id="c0e30-390">Add the **PlaceAnalysisLabel()** and **SetTagsToLastLabel()** methods, which will spawn and display the data from the Custom Vision Service into the scene.</span></span>

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

10. <span data-ttu-id="c0e30-391">Enfin, ajoutez le **CreateTrainingUI()** (méthode), ce qui génèrera l’interface utilisateur affichant les plusieurs étapes du processus de formation lors de l’application est en Mode d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="c0e30-391">Lastly, add the **CreateTrainingUI()** method, which will spawn the UI displaying the multiple stages of the training process when the application is in Training Mode.</span></span> <span data-ttu-id="c0e30-392">Cette méthode sera également être amenée à créer l’objet d’état de la caméra.</span><span class="sxs-lookup"><span data-stu-id="c0e30-392">This method will also be harnessed to create the camera status object.</span></span>

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

11. <span data-ttu-id="c0e30-393">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-393">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c0e30-394">Avant de continuer, ouvrez le **CustomVisionAnalyser** (classe) et dans le **AnalyseLastImageCaptured()** (méthode), *Décommentez* les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="c0e30-394">Before you continue, open the **CustomVisionAnalyser** class, and within the **AnalyseLastImageCaptured()** method, *uncomment* the following lines:</span></span>
>
> ```csharp
>   AnalysisObject analysisObject = new AnalysisObject();
>   analysisObject = JsonConvert.DeserializeObject<AnalysisObject>(jsonResponse);
>   SceneOrganiser.Instance.SetTagsToLastLabel(analysisObject);
> ```

## <a name="chapter-11---create-the-imagecapture-class"></a><span data-ttu-id="c0e30-395">Chapitre 11 - créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="c0e30-395">Chapter 11 - Create the ImageCapture class</span></span>

<span data-ttu-id="c0e30-396">La classe suivante, vous allez créer est la *ImageCapture* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-396">The next class you are going to create is the *ImageCapture* class.</span></span>

<span data-ttu-id="c0e30-397">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="c0e30-397">This class is responsible for:</span></span>

-   <span data-ttu-id="c0e30-398">Capture d’une image à l’aide de l’appareil photo HoloLens et en le stockant dans le *application* dossier.</span><span class="sxs-lookup"><span data-stu-id="c0e30-398">Capturing an image using the HoloLens camera and storing it in the *App* Folder.</span></span>

-   <span data-ttu-id="c0e30-399">Gestion des gestes de drainage de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-399">Handling Tap gestures from the user.</span></span>

-   <span data-ttu-id="c0e30-400">Maintenir la *Enum* valeur qui détermine si l’application s’exécutera *Analysis* mode ou *formation* Mode.</span><span class="sxs-lookup"><span data-stu-id="c0e30-400">Maintaining the *Enum* value that determines if the application will run in *Analysis* mode or *Training* Mode.</span></span>

<span data-ttu-id="c0e30-401">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="c0e30-401">To create this class:</span></span>

1.  <span data-ttu-id="c0e30-402">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="c0e30-402">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="c0e30-403">Avec le bouton droit dans le dossier, puis cliquez sur **créer > C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-403">Right-click inside the folder, then click **Create > C\# Script**.</span></span> <span data-ttu-id="c0e30-404">Nommez le script *ImageCapture*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-404">Name the script *ImageCapture*.</span></span>

3.  <span data-ttu-id="c0e30-405">Double-cliquez sur le nouveau **ImageCapture** script pour l’ouvrir avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-405">Double-click on the new **ImageCapture** script to open it with **Visual Studio**.</span></span>

4.  <span data-ttu-id="c0e30-406">Remplacez les espaces de noms en haut du fichier avec les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="c0e30-406">Replace the namespaces at the top of the file with the following:</span></span>

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="c0e30-407">Puis ajoutez les variables suivantes à l’intérieur de la *ImageCapture* classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="c0e30-407">Then add the following variables inside the *ImageCapture* class, above the **Start()** method:</span></span>

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

6.  <span data-ttu-id="c0e30-408">Code pour **Awake()** et **Start()** méthodes doit maintenant être ajouté :</span><span class="sxs-lookup"><span data-stu-id="c0e30-408">Code for **Awake()** and **Start()** methods now needs to be added:</span></span>

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

7.  <span data-ttu-id="c0e30-409">Implémentez un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit.</span><span class="sxs-lookup"><span data-stu-id="c0e30-409">Implement a handler that will be called when a Tap gesture occurs.</span></span>

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
    > <span data-ttu-id="c0e30-410">Dans *Analysis* mode, le **TapHandler** méthode agit comme un commutateur pour démarrer ou arrêter la boucle de capture photo.</span><span class="sxs-lookup"><span data-stu-id="c0e30-410">In *Analysis* mode, the **TapHandler** method acts as a switch to start or stop the photo capture loop.</span></span>
    >
    > <span data-ttu-id="c0e30-411">Dans *formation* mode, il capture une image à partir de l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="c0e30-411">In *Training* mode, it will capture an image from the camera.</span></span>
    >
    > <span data-ttu-id="c0e30-412">Lorsque le curseur est vert, cela signifie que l’appareil photo est disponible pour la prise de l’image.</span><span class="sxs-lookup"><span data-stu-id="c0e30-412">When the cursor is green, it means the camera is available to take the image.</span></span>
    >
    > <span data-ttu-id="c0e30-413">Lorsque le curseur est rouge, cela signifie que l’appareil photo est occupé.</span><span class="sxs-lookup"><span data-stu-id="c0e30-413">When the cursor is red, it means the camera is busy.</span></span>

8.  <span data-ttu-id="c0e30-414">Ajoutez la méthode que l’application utilise pour démarrer le processus de capture d’image et de stocker l’image.</span><span class="sxs-lookup"><span data-stu-id="c0e30-414">Add the method that the application uses to start the image capture process and store the image.</span></span>

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

9.  <span data-ttu-id="c0e30-415">Ajoutez les gestionnaires qui seront appelées lorsque la photo a été capturée et quand il est prêt à être analysés.</span><span class="sxs-lookup"><span data-stu-id="c0e30-415">Add the handlers that will be called when the photo has been captured and for when it is ready to be analyzed.</span></span> <span data-ttu-id="c0e30-416">Le résultat est ensuite transmis à la *CustomVisionAnalyser* ou *CustomVisionTrainer* selon le mode que le code est défini sur.</span><span class="sxs-lookup"><span data-stu-id="c0e30-416">The result is then passed to the *CustomVisionAnalyser* or the *CustomVisionTrainer* depending on which mode the code is set on.</span></span>

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

10. <span data-ttu-id="c0e30-417">Veillez à enregistrer vos modifications dans **Visual Studio** avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-417">Be sure to save your changes in **Visual Studio** before returning to **Unity**.</span></span>

11. <span data-ttu-id="c0e30-418">Maintenant que tous les scripts ont été terminés, revenez dans l’éditeur Unity, puis cliquez et faites glisser le **SceneOrganiser** classe à partir de la **Scripts** dossier pour le **Main Camera** objet dans le *hiérarchie panneau*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-418">Now that all the scripts have been completed, go back in the Unity Editor, then click and drag the **SceneOrganiser** class from the **Scripts** folder to the **Main Camera** object in the *Hierarchy Panel*.</span></span>

## <a name="chapter-12---before-building"></a><span data-ttu-id="c0e30-419">Chapitre 12 - avant la génération</span><span class="sxs-lookup"><span data-stu-id="c0e30-419">Chapter 12 - Before building</span></span>

<span data-ttu-id="c0e30-420">Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c0e30-420">To perform a thorough test of your application you will need to sideload it onto your HoloLens.</span></span>

<span data-ttu-id="c0e30-421">Avant de procéder, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="c0e30-421">Before you do, ensure that:</span></span>

- <span data-ttu-id="c0e30-422">Tous les paramètres mentionnés dans le [chapitre 2](#chapter-2---training-your-custom-vision-project) sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="c0e30-422">All the settings mentioned in the [Chapter 2](#chapter-2---training-your-custom-vision-project) are set correctly.</span></span>

- <span data-ttu-id="c0e30-423">Tous les champs dans le **Main Camera**, panneau Inspecteur, sont affectées correctement.</span><span class="sxs-lookup"><span data-stu-id="c0e30-423">All the fields in the **Main Camera**, Inspector Panel, are assigned properly.</span></span>

- <span data-ttu-id="c0e30-424">Le script **SceneOrganiser** est attaché à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="c0e30-424">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span>

- <span data-ttu-id="c0e30-425">Assurez-vous que vous insérez votre **prédiction clé** dans le **predictionKey** variable.</span><span class="sxs-lookup"><span data-stu-id="c0e30-425">Make sure you insert your **Prediction Key** into the **predictionKey** variable.</span></span>

- <span data-ttu-id="c0e30-426">Vous avez inséré votre **point de terminaison de prédiction** dans le **predictionEndpoint** variable.</span><span class="sxs-lookup"><span data-stu-id="c0e30-426">You have inserted your **Prediction Endpoint** into the **predictionEndpoint** variable.</span></span>

- <span data-ttu-id="c0e30-427">Vous avez inséré votre **formation clé** dans le **trainingKey** variable, de la *CustomVisionTrainer* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-427">You have inserted your **Training Key** into the **trainingKey** variable, of the *CustomVisionTrainer* class.</span></span>

- <span data-ttu-id="c0e30-428">Vous avez inséré votre **ID de projet** dans le **projectId** variable, de la *CustomVisionTrainer* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-428">You have inserted your **Project ID** into the **projectId** variable, of the *CustomVisionTrainer* class.</span></span>

## <a name="chapter-13---build-and-sideload-your-application"></a><span data-ttu-id="c0e30-429">Chapitre 13 - Build et chargement de version test votre application</span><span class="sxs-lookup"><span data-stu-id="c0e30-429">Chapter 13 - Build and sideload your application</span></span>

<span data-ttu-id="c0e30-430">Pour commencer le *Build* processus :</span><span class="sxs-lookup"><span data-stu-id="c0e30-430">To begin the *Build* process:</span></span>

1.  <span data-ttu-id="c0e30-431">Accédez à **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-431">Go to **File > Build Settings**.</span></span>

2.  <span data-ttu-id="c0e30-432">Graduation **Unity C\# projets**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-432">Tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="c0e30-433">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-433">Click **Build**.</span></span> <span data-ttu-id="c0e30-434">Unity lancera un **Explorateur de fichiers** fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="c0e30-434">Unity will launch a **File Explorer** window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="c0e30-435">Créez ce dossier, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-435">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="c0e30-436">Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-436">Then with the **App** folder selected, click on **Select Folder**.</span></span>

4.  <span data-ttu-id="c0e30-437">Unity commencera à générer votre projet pour le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="c0e30-437">Unity will begin building your project to the **App** folder.</span></span>

5.  <span data-ttu-id="c0e30-438">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="c0e30-438">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

<span data-ttu-id="c0e30-439">Pour déployer sur HoloLens :</span><span class="sxs-lookup"><span data-stu-id="c0e30-439">To deploy on HoloLens:</span></span>

1.  <span data-ttu-id="c0e30-440">Vous devez l’adresse IP de votre HoloLens (pour les déployer à distance) et pour vérifier que votre HoloLens est dans **Mode développeur**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-440">You will need the IP Address of your HoloLens (for Remote Deploy), and to ensure your HoloLens is in **Developer Mode**.</span></span> <span data-ttu-id="c0e30-441">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="c0e30-441">To do this:</span></span>

    1.  <span data-ttu-id="c0e30-442">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-442">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="c0e30-443">Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**</span><span class="sxs-lookup"><span data-stu-id="c0e30-443">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="c0e30-444">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="c0e30-444">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="c0e30-445">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="c0e30-445">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="c0e30-446">Définissez **Mode développeur sur**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-446">Set **Developer Mode On**.</span></span>

2.  <span data-ttu-id="c0e30-447">Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-447">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

3.  <span data-ttu-id="c0e30-448">Dans le *Configuration de la Solution* sélectionnez **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-448">In the *Solution Configuration* select **Debug**.</span></span>

4.  <span data-ttu-id="c0e30-449">Dans le *plateforme de Solution*, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-449">In the *Solution Platform*, select **x86, Remote Machine**.</span></span> <span data-ttu-id="c0e30-450">Vous devrez insérer le **adresse IP** d’un appareil à distance (la HoloLens, dans ce cas, que vous avez notée).</span><span class="sxs-lookup"><span data-stu-id="c0e30-450">You will be prompted to insert the **IP address** of a remote device (the HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab302b-34.png)

5. <span data-ttu-id="c0e30-451">Accédez à **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="c0e30-451">Go to **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

6. <span data-ttu-id="c0e30-452">Votre application doit maintenant apparaître dans la liste des applications installées sur votre HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="c0e30-452">Your app should now appear in the list of installed apps on your HoloLens, ready to be launched!</span></span>

> [!NOTE]
> <span data-ttu-id="c0e30-453">Pour déployer sur casque immersif, définissez le **plateforme de Solution** à *ordinateur Local*et définissez le **Configuration** à *déboguer*, avec *x86* en tant que le **plateforme**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-453">To deploy to immersive headset, set the **Solution Platform** to *Local Machine*, and set the **Configuration** to *Debug*, with *x86* as the **Platform**.</span></span> <span data-ttu-id="c0e30-454">Déployer sur l’ordinateur local d’ordinateur, à l’aide de la **Build** élément de menu, en sélectionnant *déployer la Solution*.</span><span class="sxs-lookup"><span data-stu-id="c0e30-454">Then deploy to the local machine, using the **Build** menu item, selecting *Deploy Solution*.</span></span> 

## <a name="to-use-the-application"></a><span data-ttu-id="c0e30-455">Pour utiliser l’application :</span><span class="sxs-lookup"><span data-stu-id="c0e30-455">To use the application:</span></span>

<span data-ttu-id="c0e30-456">Pour basculer de la fonctionnalité d’application entre *formation* mode et *prédiction* mode, vous devez mettre à jour le **AppMode** variable, qui se trouve dans le **Awake()** méthode situés dans le *ImageCapture* classe.</span><span class="sxs-lookup"><span data-stu-id="c0e30-456">To switch the app functionality between *Training* mode and *Prediction* mode you need to update the **AppMode** variable, located in the **Awake()** method located within the *ImageCapture* class.</span></span>

```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Training;
```
<span data-ttu-id="c0e30-457">ou Gestionnaire de configuration</span><span class="sxs-lookup"><span data-stu-id="c0e30-457">or</span></span>
```
        // Change this flag to switch between Analysis mode and Training mode 
        AppMode = AppModes.Analysis;
```

<span data-ttu-id="c0e30-458">Dans *formation* mode :</span><span class="sxs-lookup"><span data-stu-id="c0e30-458">In *Training* mode:</span></span>

- <span data-ttu-id="c0e30-459">Examinez **souris** ou **clavier** et utiliser le **mouvement d’appui**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-459">Look at **Mouse** or **Keyboard** and use the **Tap gesture**.</span></span>

- <span data-ttu-id="c0e30-460">Ensuite, le texte s’affiche vous demandant de fournir une balise.</span><span class="sxs-lookup"><span data-stu-id="c0e30-460">Next, text will appear asking you to provide a tag.</span></span>

- <span data-ttu-id="c0e30-461">Indiquer **souris** ou **clavier**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-461">Say either **Mouse** or **Keyboard**.</span></span>


<span data-ttu-id="c0e30-462">Dans *prédiction* mode :</span><span class="sxs-lookup"><span data-stu-id="c0e30-462">In *Prediction* mode:</span></span>

- <span data-ttu-id="c0e30-463">Rechercher un objet et d’utiliser le **mouvement d’appui**.</span><span class="sxs-lookup"><span data-stu-id="c0e30-463">Look at an object and use the **Tap gesture**.</span></span>

- <span data-ttu-id="c0e30-464">Texte s’affiche en fournissant l’objet détecté, avec la probabilité la plus élevée (cela est normalisé).</span><span class="sxs-lookup"><span data-stu-id="c0e30-464">Text will appear providing the object detected, with the highest probability (this is normalized).</span></span>

## <a name="chapter-14---evaluate-and-improve-your-custom-vision-model"></a><span data-ttu-id="c0e30-465">Chapitre 14 - évaluer et améliorer votre modèle de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="c0e30-465">Chapter 14 - Evaluate and improve your Custom Vision model</span></span>

<span data-ttu-id="c0e30-466">Pour rendre la plus précise de votre Service, vous devrez continuer à former le modèle utilisé pour la prédiction.</span><span class="sxs-lookup"><span data-stu-id="c0e30-466">To make your Service more accurate, you will need to continue to train the model used for prediction.</span></span> <span data-ttu-id="c0e30-467">Ceci est réalisé grâce à l’aide de votre nouvelle application, avec à la fois le *formation* et *prédiction* modes, avec le dernier que vous ayez à visiter le portail, c'est-à-dire des sujets traités dans ce chapitre.</span><span class="sxs-lookup"><span data-stu-id="c0e30-467">This is accomplished through using your new application, with both the *training* and *prediction* modes, with the latter requiring you to visit the portal, which is what is covered in this Chapter.</span></span> <span data-ttu-id="c0e30-468">Soyez prêt à revenir sur votre portail plusieurs fois, afin d’améliorer en permanence votre modèle.</span><span class="sxs-lookup"><span data-stu-id="c0e30-468">Be prepared to revisit your portal many times, to continually improve your model.</span></span>

1. <span data-ttu-id="c0e30-469">Accédez à nouveau à votre portail de Vision personnalisée Azure et une fois que vous êtes dans votre projet, sélectionnez le *prédictions* onglet (à partir de centre du bord supérieur de la page) :</span><span class="sxs-lookup"><span data-stu-id="c0e30-469">Head to your Azure Custom Vision Portal again, and once you are in your project, select the *Predictions* tab (from the top center of the page):</span></span>

    ![](images/AzureLabs-Lab302b-35.png)

2. <span data-ttu-id="c0e30-470">Vous verrez toutes les images qui ont été envoyés à votre Service, tandis que votre application a été exécutée.</span><span class="sxs-lookup"><span data-stu-id="c0e30-470">You will see all the images which were sent to your Service whilst your application was running.</span></span> <span data-ttu-id="c0e30-471">Si vous pointez sur les images, ils vous fournira les prédictions qui ont été apportées pour cette image :</span><span class="sxs-lookup"><span data-stu-id="c0e30-471">If you hover over the images, they will provide you with the predictions that were made for that image:</span></span>

    ![](images/AzureLabs-Lab302b-36.png)

3. <span data-ttu-id="c0e30-472">Sélectionnez une de vos images pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="c0e30-472">Select one of your images to open it.</span></span> <span data-ttu-id="c0e30-473">Une fois ouvert, vous verrez les prévisions effectuées pour cette image vers la droite.</span><span class="sxs-lookup"><span data-stu-id="c0e30-473">Once open, you will see the predictions made for that image to the right.</span></span> <span data-ttu-id="c0e30-474">Si vous la justesse des prédictions correctes et que vous souhaitez ajouter cette image à un modèle d’apprentissage de votre Service, cliquez sur le *Mes balises* zone d’entrée, puis sélectionnez la balise que vous souhaitez associer.</span><span class="sxs-lookup"><span data-stu-id="c0e30-474">If you the predictions were correct, and you wish to add this image to your Service's training model, click the *My Tags* input box, and select the tag you wish to associate.</span></span> <span data-ttu-id="c0e30-475">Lorsque vous avez terminé, cliquez sur le *enregistrer et fermer* bouton en bas à droite et de passer à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="c0e30-475">When you are finished, click the *Save and close* button to the bottom right, and continue on to the next image.</span></span>

    ![](images/AzureLabs-Lab302b-37.png)

4. <span data-ttu-id="c0e30-476">Une fois que vous êtes à la grille des images, vous remarquerez les images que vous avez ajouté des balises à (et enregistré), va être supprimé.</span><span class="sxs-lookup"><span data-stu-id="c0e30-476">Once you are back to the grid of images, you will notice the images which you have added tags to (and saved), will be removed.</span></span> <span data-ttu-id="c0e30-477">Si vous trouvez des images que vous pensez ne pas votre élément balisé en leur sein, vous pouvez les supprimer, en cliquant sur les graduations sur cette image (cette opération pour plusieurs images), puis sur *supprimer* dans le coin supérieur droit de la page de grille.</span><span class="sxs-lookup"><span data-stu-id="c0e30-477">If you find any images which you think do not have your tagged item within them, you can delete them, by clicking the tick on that image (can do this for several images) and then clicking *Delete* in the upper right corner of the grid page.</span></span> <span data-ttu-id="c0e30-478">Dans la fenêtre contextuelle qui suit, vous pouvez cliquer sur *Oui, supprimer* ou *non*, pour confirmer la suppression ou de l’annuler, respectivement.</span><span class="sxs-lookup"><span data-stu-id="c0e30-478">On the popup that follows, you can click either *Yes, delete* or *No*, to confirm the deletion or cancel it, respectively.</span></span> 

    ![](images/AzureLabs-Lab302b-38.png)

5. <span data-ttu-id="c0e30-479">Lorsque vous êtes prêt à continuer, cliquez sur le vert *Train* bouton dans le coin supérieur droit.</span><span class="sxs-lookup"><span data-stu-id="c0e30-479">When you are ready to proceed, click the green *Train* button in the top right.</span></span> <span data-ttu-id="c0e30-480">Votre modèle de Service sera formé avec toutes les images que vous avez maintenant fourni (ce qui rendent plus précis).</span><span class="sxs-lookup"><span data-stu-id="c0e30-480">Your Service model will be trained with all the images which you have now provided (which will make it more accurate).</span></span> <span data-ttu-id="c0e30-481">Une fois la formation terminée, veillez à cliquer sur le *par défaut* bouton une fois de plus, afin que votre *prédiction URL* continue d’utiliser l’itération la plus récente de votre Service.</span><span class="sxs-lookup"><span data-stu-id="c0e30-481">Once the training is complete, make sure to click the *Make default* button once more, so that your *Prediction URL* continues to use the most up-to-date iteration of your Service.</span></span>

    <span data-ttu-id="c0e30-482">![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)</span><span class="sxs-lookup"><span data-stu-id="c0e30-482">![](images/AzureLabs-Lab302b-39.png) ![](images/AzureLabs-Lab302b-40.png)</span></span>

## <a name="your-finished-custom-vision-api-application"></a><span data-ttu-id="c0e30-483">Votre application API de Vision personnalisée terminée</span><span class="sxs-lookup"><span data-stu-id="c0e30-483">Your finished Custom Vision API application</span></span>

<span data-ttu-id="c0e30-484">Félicitations, vous avez créé une application de réalité mixte qui tire parti de l’API de Vision Azure personnalisée pour reconnaître des objets du monde réel, former le modèle de Service et afficher le niveau de confiance de ce qui a été vu.</span><span class="sxs-lookup"><span data-stu-id="c0e30-484">Congratulations, you built a mixed reality app that leverages the Azure Custom Vision API to recognize real world objects, train the Service model, and display confidence of what has been seen.</span></span>

![](images/AzureLabs-Lab302b-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="c0e30-485">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="c0e30-485">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="c0e30-486">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="c0e30-486">Exercise 1</span></span>

<span data-ttu-id="c0e30-487">Former votre **Service Vision personnalisée** à reconnaître plus d’objets.</span><span class="sxs-lookup"><span data-stu-id="c0e30-487">Train your **Custom Vision Service** to recognize more objects.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="c0e30-488">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="c0e30-488">Exercise 2</span></span>

<span data-ttu-id="c0e30-489">Comme un moyen pour développer ce que vous avez appris, effectuez les exercices suivants :</span><span class="sxs-lookup"><span data-stu-id="c0e30-489">As a way to expand on what you have learned, complete the following exercises:</span></span>

<span data-ttu-id="c0e30-490">Un signal sonore lorsqu’un objet est reconnu.</span><span class="sxs-lookup"><span data-stu-id="c0e30-490">Play a sound when an object is recognized.</span></span>

### <a name="exercise-3"></a><span data-ttu-id="c0e30-491">Exercice 3</span><span class="sxs-lookup"><span data-stu-id="c0e30-491">Exercise 3</span></span>

<span data-ttu-id="c0e30-492">Utiliser l’API pour recalculer votre Service avec les mêmes images de l’analyse de votre application, par conséquent, pour rendre le Service plus précis (effectuer la prédiction et la formation simultanément).</span><span class="sxs-lookup"><span data-stu-id="c0e30-492">Use the API to re-train your Service with the same images your app is analyzing, so to make the Service more accurate (do both prediction and training simultaneously).</span></span>
