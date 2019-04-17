---
title: MR et 310 Azure - détection d’objets
description: Effectuez ce cours pour apprendre à former un modèle d’apprentissage, puis utilisez le modèle formé pour reconnaître des objets similaires et leur position dans le monde réel à partir d’une application de réalité mixte.
author: drneil
ms.author: jemccull
ms.date: 07/04/2018
ms.topic: article
keywords: Azure, vision personnalisée, l’objet de détection, mixte réalité academy, unity, didacticiel, api, hololens
ms.openlocfilehash: 89ee79943a88de8a34c679ae33621db5770908b0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593286"
---
>[!NOTE]
><span data-ttu-id="10f2d-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="10f2d-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="10f2d-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="10f2d-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="10f2d-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="10f2d-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="10f2d-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="10f2d-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="10f2d-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="10f2d-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="10f2d-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="10f2d-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-310-object-detection"></a><span data-ttu-id="10f2d-110">MR et Azure 310 : Détection d’objets</span><span class="sxs-lookup"><span data-stu-id="10f2d-110">Mr and Azure 310: Object detection</span></span>

<span data-ttu-id="10f2d-111">Dans ce cours, vous allez apprendre à reconnaître le contenu visuel personnalisé et sa position spatiale dans une image fournie, à l’aide de Vision personnalisée Azure des fonctionnalités de « Détection d’objets » dans une application de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="10f2d-111">In this course, you will learn how to recognize custom visual content and its spatial position within a provided image, using Azure Custom Vision "Object Detection" capabilities in a mixed reality application.</span></span>

<span data-ttu-id="10f2d-112">Ce service vous permettra de former un modèle d’apprentissage automatique à l’aide d’images de l’objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-112">This service will allow you to train a machine learning model using object images.</span></span> <span data-ttu-id="10f2d-113">Vous allez utiliser ensuite le modèle formé pour reconnaître des objets similaires et se rapprocher de leur emplacement dans le monde réel, tel que fourni par la capture de l’appareil photo de Microsoft HoloLens ou une caméra de se connecter à un PC pour des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="10f2d-113">You will then use the trained model to recognize similar objects and approximate their location in the real world, as provided by the camera capture of Microsoft HoloLens or a camera connect to a PC for immersive (VR) headsets.</span></span>

![résultat de cours](images/AzureLabs-Lab310-00.png)

<span data-ttu-id="10f2d-115">**Vision personnalisée Azure, la détection d’objets** est un Service Microsoft qui permet aux développeurs de créer des classifieurs de l’image personnalisée.</span><span class="sxs-lookup"><span data-stu-id="10f2d-115">**Azure Custom Vision, Object Detection** is a Microsoft Service which allows developers to build custom image classifiers.</span></span> <span data-ttu-id="10f2d-116">Ces classifieurs peuvent ensuite servir avec les nouvelles images pour détecter des objets au sein de cette nouvelle image, en fournissant **limites de la zone** dans l’image elle-même.</span><span class="sxs-lookup"><span data-stu-id="10f2d-116">These classifiers can then be used with new images to detect objects within that new image, by providing **Box Boundaries** within the image itself.</span></span> <span data-ttu-id="10f2d-117">Le Service fournit un portail en ligne simple et facile à utiliser, pour simplifier ce processus.</span><span class="sxs-lookup"><span data-stu-id="10f2d-117">The Service provides a simple, easy to use, online portal to streamline this process.</span></span> <span data-ttu-id="10f2d-118">Pour plus d’informations, consultez les liens suivants :</span><span class="sxs-lookup"><span data-stu-id="10f2d-118">For more information, visit the following links:</span></span>

* [<span data-ttu-id="10f2d-119">Page de Vision personnalisée Azure</span><span class="sxs-lookup"><span data-stu-id="10f2d-119">Azure Custom Vision page</span></span>](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/home)
* [<span data-ttu-id="10f2d-120">Limites et Quotas</span><span class="sxs-lookup"><span data-stu-id="10f2d-120">Limits and Quotas</span></span>](https://docs.microsoft.com/azure/cognitive-services/custom-vision-service/limits-and-quotas)

<span data-ttu-id="10f2d-121">À la fin de ce cours, vous disposez d’une application de réalité mixte qui sera en mesure d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="10f2d-121">Upon completion of this course, you will have a mixed reality application which will be able to do the following:</span></span>

1. <span data-ttu-id="10f2d-122">L’utilisateur sera en mesure de *les regards* à un objet, ils ont formé à l’aide de Azure Custom Vision Service, détection d’objets.</span><span class="sxs-lookup"><span data-stu-id="10f2d-122">The user will be able to *gaze* at an object, which they have trained using the Azure Custom Vision Service, Object Detection.</span></span> 
2. <span data-ttu-id="10f2d-123">L’utilisateur utilisera la *appuyez sur* mouvement à capturer une image de ce qu’ils cherchent à.</span><span class="sxs-lookup"><span data-stu-id="10f2d-123">The user will use the *Tap* gesture to capture an image of what they are looking at.</span></span>
3. <span data-ttu-id="10f2d-124">L’application envoie l’image à Azure Custom Vision Service.</span><span class="sxs-lookup"><span data-stu-id="10f2d-124">The app will send the image to the Azure Custom Vision Service.</span></span>
4. <span data-ttu-id="10f2d-125">Il y aura une réponse à partir du Service qui affiche le résultat de la reconnaissance en tant que texte de l’espace universel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-125">There will be a reply from the Service which will display the result of the recognition as world-space text.</span></span> <span data-ttu-id="10f2d-126">Cela doit être effectué via l’utilisation spatiale de suivi du Microsoft HoloLens, comme un moyen de comprendre la position du monde de l’objet reconnu, puis en utilisant le *balise* associé à ce qui est détecté dans l’image, à fournir le texte d’étiquette.</span><span class="sxs-lookup"><span data-stu-id="10f2d-126">This will be accomplished through utilizing the Microsoft HoloLens' Spatial Tracking, as a way of understanding the world position of the recognized object, and then using the *Tag* associated with what is detected in the image, to provide the label text.</span></span>

<span data-ttu-id="10f2d-127">Ce cours couvre également manuellement durant le chargement d’images, création de balises, et de formation au Service, à reconnaître différents objets (dans l’exemple fourni, une tasse), en définissant le *boîte limite* au sein de l’image que vous envoyez.</span><span class="sxs-lookup"><span data-stu-id="10f2d-127">The course will also cover manually uploading images, creating tags, and training the Service, to recognize different objects (in the provided example, a cup), by setting the *Boundary Box* within the image you submit.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="10f2d-128">Après la création et l’utilisation de l’application, le développeur doit revenir à Azure Custom Vision Service et d’identifier les prédictions générées par le Service et déterminer si elles ont été correctes ou non (par le biais de balisage quoi que ce soit le Service manquée, et ajuster la *englobants*).</span><span class="sxs-lookup"><span data-stu-id="10f2d-128">Following the creation and use of the app, the developer should navigate back to the Azure Custom Vision Service, and identify the predictions made by the Service, and determine whether they were correct or not (through tagging anything the Service missed, and adjusting the *Bounding Boxes*).</span></span> <span data-ttu-id="10f2d-129">Le Service peut ensuite être ré-formé, ce qui augmente la probabilité qu’il reconnaissance des objets du monde réel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-129">The Service can then be re-trained, which will increase the likelihood of it recognizing real world objects.</span></span>

<span data-ttu-id="10f2d-130">Ce cours va vous apprendre à obtenir les résultats à partir de Azure Custom Vision Service, détection d’objets, dans une application basée sur Unity.</span><span class="sxs-lookup"><span data-stu-id="10f2d-130">This course will teach you how to get the results from the Azure Custom Vision Service, Object Detection, into a Unity-based sample application.</span></span> <span data-ttu-id="10f2d-131">Il le sera jusqu'à vous permettent d’appliquer ces concepts à une application personnalisée, que vous voudrez peut-être générer.</span><span class="sxs-lookup"><span data-stu-id="10f2d-131">It will be up to you to apply these concepts to a custom application you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="10f2d-132">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="10f2d-132">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="10f2d-133">Cours</span><span class="sxs-lookup"><span data-stu-id="10f2d-133">Course</span></span></th><th style="width:150px"> <span data-ttu-id="10f2d-134"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="10f2d-134"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="10f2d-135"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="10f2d-135"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="10f2d-136">MR et Azure 310 : Détection d’objets</span><span class="sxs-lookup"><span data-stu-id="10f2d-136">MR and Azure 310: Object detection</span></span></td><td style="text-align: center;"> <span data-ttu-id="10f2d-137">✔️</span><span class="sxs-lookup"><span data-stu-id="10f2d-137">✔️</span></span></td><td style="text-align: center;"> </td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="10f2d-138">Prérequis</span><span class="sxs-lookup"><span data-stu-id="10f2d-138">Prerequisites</span></span>

> [!NOTE]
> <span data-ttu-id="10f2d-139">Ce didacticiel est conçu pour les développeurs qui ont une expérience basique avec Unity et C#.</span><span class="sxs-lookup"><span data-stu-id="10f2d-139">This tutorial is designed for developers who have basic experience with Unity and C#.</span></span> <span data-ttu-id="10f2d-140">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="10f2d-140">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="10f2d-141">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récent que celui indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="10f2d-141">You are free to use the latest software, as listed within the [install the tools](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than what is listed below.</span></span>

<span data-ttu-id="10f2d-142">Nous recommandons le matériel et logiciel pour ce cours suivants :</span><span class="sxs-lookup"><span data-stu-id="10f2d-142">We recommend the following hardware and software for this course:</span></span>

- <span data-ttu-id="10f2d-143">Un PC de développement</span><span class="sxs-lookup"><span data-stu-id="10f2d-143">A development PC</span></span>
- [<span data-ttu-id="10f2d-144">Windows 10 Fall Creators Update (ou version ultérieure) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="10f2d-144">Windows 10 Fall Creators Update (or later) with Developer mode enabled</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="10f2d-145">Le SDK Windows 10 dernières</span><span class="sxs-lookup"><span data-stu-id="10f2d-145">The latest Windows 10 SDK</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="10f2d-146">Unity 2017.4 LTS</span><span class="sxs-lookup"><span data-stu-id="10f2d-146">Unity 2017.4 LTS</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- [<span data-ttu-id="10f2d-147">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="10f2d-147">Visual Studio 2017</span></span>](https://docs.microsoft.com/windows/mixed-reality/install-the-tools#installation-checklist-for-hololens)
- <span data-ttu-id="10f2d-148">Un [Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) avec le mode développeur est activé</span><span class="sxs-lookup"><span data-stu-id="10f2d-148">A [Microsoft HoloLens](https://docs.microsoft.com/windows/mixed-reality/hololens-hardware-details) with Developer mode enabled</span></span>
- <span data-ttu-id="10f2d-149">Accès à Internet pour le programme d’installation Azure et de récupération du Service Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="10f2d-149">Internet access for Azure setup and Custom Vision Service retrieval</span></span>
-  <span data-ttu-id="10f2d-150">Une série d’images au moins quinze (15) sont nécessaires) pour chaque objet que vous souhaitez que la Vision personnalisée pour reconnaître.</span><span class="sxs-lookup"><span data-stu-id="10f2d-150">A series of at least fifteen (15) images are required) for each object that you would like the Custom Vision to recognize.</span></span> <span data-ttu-id="10f2d-151">Si vous le souhaitez, vous pouvez utiliser les images déjà fournis avec ce cours, [une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span><span class="sxs-lookup"><span data-stu-id="10f2d-151">If you wish, you can use the images already provided with this course, [a series of cups](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span></span>

## <a name="before-you-start"></a><span data-ttu-id="10f2d-152">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="10f2d-152">Before you start</span></span>

1.  <span data-ttu-id="10f2d-153">Pour éviter de rencontrer des problèmes de création de ce projet, il est fortement recommandé que vous créez le projet mentionné dans ce didacticiel dans un dossier racine ou près de racine (chemins d’accès de dossier long peuvent entraîner des problèmes au moment de la génération).</span><span class="sxs-lookup"><span data-stu-id="10f2d-153">To avoid encountering issues building this project, it is strongly suggested that you create the project mentioned in this tutorial in a root or near-root folder (long folder paths can cause issues at build-time).</span></span>
2.  <span data-ttu-id="10f2d-154">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="10f2d-154">Set up and test your HoloLens.</span></span> <span data-ttu-id="10f2d-155">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="10f2d-155">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span> 
3.  <span data-ttu-id="10f2d-156">Il est judicieux d’effectuer l’étalonnage et le réglage de capteur lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="10f2d-156">It is a good idea to perform Calibration and Sensor Tuning when beginning developing a new HoloLens App (sometimes it can help to perform those tasks for each user).</span></span> 

<span data-ttu-id="10f2d-157">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="10f2d-157">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="10f2d-158">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="10f2d-158">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

## <a name="chapter-1---the-custom-vision-portal"></a><span data-ttu-id="10f2d-159">Chapitre 1 : le portail de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="10f2d-159">Chapter 1 - The Custom Vision Portal</span></span>

<span data-ttu-id="10f2d-160">Pour utiliser le **Azure Custom Vision Service**, vous devez configurer une instance de celle-ci à la disposition de votre application.</span><span class="sxs-lookup"><span data-stu-id="10f2d-160">To use the **Azure Custom Vision Service**, you will need to configure an instance of it to be made available to your application.</span></span>

1.  <span data-ttu-id="10f2d-161">Accédez [à la **Service Vision personnalisée** page principale](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span><span class="sxs-lookup"><span data-stu-id="10f2d-161">Navigate [to the **Custom Vision Service** main page](https://azure.microsoft.com/services/cognitive-services/custom-vision-service/).</span></span>

2.  <span data-ttu-id="10f2d-162">Cliquez sur **mise en route**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-162">Click on **Getting Started**.</span></span>

    ![](images/AzureLabs-Lab310-01.png)

3.  <span data-ttu-id="10f2d-163">Connectez-vous au portail de Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="10f2d-163">Sign in to the Custom Vision Portal.</span></span>

    ![](images/AzureLabs-Lab310-02.png)

4.  <span data-ttu-id="10f2d-164">Si vous n’avez pas déjà un compte Azure, vous devrez créer un.</span><span class="sxs-lookup"><span data-stu-id="10f2d-164">If you do not already have an Azure account, you will need to create one.</span></span> <span data-ttu-id="10f2d-165">Si vous suivez ce didacticiel dans une situation de laboratoire ou salle de classe, demandez à votre formateur ou celui des surveillants pour la configuration de votre nouveau compte.</span><span class="sxs-lookup"><span data-stu-id="10f2d-165">If you are following this tutorial in a classroom or lab situation, ask your instructor or one of the proctors for help setting up your new account.</span></span>

5.  <span data-ttu-id="10f2d-166">Une fois que vous êtes connecté pour la première fois, vous serez invité au *termes du contrat de Service* Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="10f2d-166">Once you are logged in for the first time, you will be prompted with the *Terms of Service* panel.</span></span> <span data-ttu-id="10f2d-167">Cliquez sur la case à cocher pour *accepte les termes du contrat*.</span><span class="sxs-lookup"><span data-stu-id="10f2d-167">Click the checkbox to *agree to the terms*.</span></span> <span data-ttu-id="10f2d-168">Puis cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-168">Then click **I agree**.</span></span>

    ![](images/AzureLabs-Lab310-03.png)

6.  <span data-ttu-id="10f2d-169">Ayant accepté les termes du contrat, vous êtes maintenant dans le *Mes projets* section.</span><span class="sxs-lookup"><span data-stu-id="10f2d-169">Having agreed to the terms, you are now in the *My Projects* section.</span></span> <span data-ttu-id="10f2d-170">Cliquez sur **nouveau projet**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-170">Click on **New Project**.</span></span>

    ![](images/AzureLabs-Lab310-04.png)

7.  <span data-ttu-id="10f2d-171">Un onglet s’affiche sur le côté droit, qui vous invite à spécifier des champs pour le projet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-171">A tab will appear on the right-hand side, which will prompt you to specify some fields for the project.</span></span>

    1.  <span data-ttu-id="10f2d-172">Insérer un nom pour votre projet</span><span class="sxs-lookup"><span data-stu-id="10f2d-172">Insert a name for your project</span></span>

    2.  <span data-ttu-id="10f2d-173">Insérer une description pour votre projet (**facultatif**)</span><span class="sxs-lookup"><span data-stu-id="10f2d-173">Insert a description for your project (**Optional**)</span></span>

    3.  <span data-ttu-id="10f2d-174">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="10f2d-174">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="10f2d-175">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="10f2d-175">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="10f2d-176">Il est recommandé de garder tous les services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="10f2d-176">It is recommended to keep all the Azure services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        ![](images/AzureLabs-Lab310-05.png)

        > [!NOTE]
        > <span data-ttu-id="10f2d-177">Si vous souhaitez [en savoir plus sur les groupes de ressources Azure, accédez à la documentation associée](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span><span class="sxs-lookup"><span data-stu-id="10f2d-177">If you wish to [read more about Azure Resource Groups, navigate to the associated Docs](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)</span></span>

    4.  <span data-ttu-id="10f2d-178">Définir le **Types de projets** comme **détection d’objets (version préliminaire)**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-178">Set the **Project Types** as **Object Detection (preview)**.</span></span>

8.  <span data-ttu-id="10f2d-179">Une fois que vous avez terminé, cliquez sur **créer un projet**, et vous êtes redirigé vers la page de projet de Service Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="10f2d-179">Once you are finished, click on **Create project**, and you will be redirected to the Custom Vision Service project page.</span></span>


## <a name="chapter-2---training-your-custom-vision-project"></a><span data-ttu-id="10f2d-180">Chapitre 2 - formation de votre projet de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="10f2d-180">Chapter 2 - Training your Custom Vision project</span></span>

<span data-ttu-id="10f2d-181">Une fois dans le portail de Vision personnalisée, votre objectif principal est pour l’apprentissage de votre projet pour reconnaître des objets spécifiques dans des images.</span><span class="sxs-lookup"><span data-stu-id="10f2d-181">Once in the Custom Vision Portal, your primary objective is to train your project to recognize specific objects in images.</span></span>

<span data-ttu-id="10f2d-182">Vous devez au moins quinze (15) les images pour chaque objet que vous souhaitez que votre application à reconnaître.</span><span class="sxs-lookup"><span data-stu-id="10f2d-182">You need at least fifteen (15) images for each object that you would like your application to recognize.</span></span> <span data-ttu-id="10f2d-183">Vous pouvez utiliser les images fournies avec ce cours ([une série de tasses](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span><span class="sxs-lookup"><span data-stu-id="10f2d-183">You can use the images provided with this course ([a series of cups](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Cup%20Images.zip)).</span></span>

<span data-ttu-id="10f2d-184">Pour l’apprentissage de votre projet de Vision personnalisée :</span><span class="sxs-lookup"><span data-stu-id="10f2d-184">To train your Custom Vision project:</span></span>

1.  <span data-ttu-id="10f2d-185">Cliquez sur le **+** situé en regard **balises**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-185">Click on the **+** button next to **Tags**.</span></span>

    ![](images/AzureLabs-Lab310-06.png)

2.  <span data-ttu-id="10f2d-186">Ajouter un **nom** pour la balise qui sera utilisée pour associer vos images avec.</span><span class="sxs-lookup"><span data-stu-id="10f2d-186">Add a **name** for the tag that will be used to associate your images with.</span></span> <span data-ttu-id="10f2d-187">Dans cet exemple, nous utilisons des images de tasses de reconnaissance, afin d’avoir nommé la balise pour ce faire, **Cup**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-187">In this example we are using images of cups for recognition, so have named the tag for this, **Cup**.</span></span> <span data-ttu-id="10f2d-188">Cliquez sur **enregistrer** une fois terminé.</span><span class="sxs-lookup"><span data-stu-id="10f2d-188">Click **Save** once finished.</span></span>

    ![](images/AzureLabs-Lab310-07.png)

3.  <span data-ttu-id="10f2d-189">Vous remarquerez votre **balise** a été ajouté (vous devrez peut-être recharger votre page pour qu’il apparaisse).</span><span class="sxs-lookup"><span data-stu-id="10f2d-189">You will notice your **Tag** has been added (you may need to reload your page for it to appear).</span></span> 

    ![](images/AzureLabs-Lab310-08.png)

4.  <span data-ttu-id="10f2d-190">Cliquez sur **ajouter des images** dans le centre de la page.</span><span class="sxs-lookup"><span data-stu-id="10f2d-190">Click on **Add images** in the center of the page.</span></span>

    ![](images/AzureLabs-Lab310-09.png)

5.  <span data-ttu-id="10f2d-191">Cliquez sur **parcourir les fichiers locaux**et cliquez sur Parcourir pour les images que vous voulez charger un objet, avec le minimum étant quinze (15).</span><span class="sxs-lookup"><span data-stu-id="10f2d-191">Click on **Browse local files**, and browse to the images you would like to upload for one object, with the minimum being fifteen (15).</span></span>

    > [!TIP]
    >  <span data-ttu-id="10f2d-192">Vous pouvez sélectionner plusieurs images à la fois, à télécharger.</span><span class="sxs-lookup"><span data-stu-id="10f2d-192">You can select several images at a time, to upload.</span></span>

    ![](images/AzureLabs-Lab310-10.png)

6.  <span data-ttu-id="10f2d-193">Appuyez sur **charger des fichiers** une fois que vous avez sélectionné toutes les images vous souhaitez effectuer le projet avec l’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="10f2d-193">Press **Upload files** once you have selected all the images you would like to train the project with.</span></span> <span data-ttu-id="10f2d-194">Les fichiers de lancer le chargement.</span><span class="sxs-lookup"><span data-stu-id="10f2d-194">The files will begin uploading.</span></span> <span data-ttu-id="10f2d-195">Une fois que vous avez la confirmation du téléchargement, cliquez sur **fait**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-195">Once you have confirmation of the upload, click **Done**.</span></span>

    ![](images/AzureLabs-Lab310-11.png)

7.  <span data-ttu-id="10f2d-196">À ce stade vos images sont téléchargées, mais pas marquées.</span><span class="sxs-lookup"><span data-stu-id="10f2d-196">At this point your images are uploaded, but not tagged.</span></span>

    ![](images/AzureLabs-Lab310-12.png)

8.  <span data-ttu-id="10f2d-197">Pour marquer vos images, utilisez votre souris.</span><span class="sxs-lookup"><span data-stu-id="10f2d-197">To tag your images, use your mouse.</span></span> <span data-ttu-id="10f2d-198">Lorsque vous pointez sur votre image, une mise en surbrillance de sélection vous aider en dessinant automatiquement une sélection autour de votre objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-198">As you hover over your image, a selection highlight will aid you by automatically drawing a selection around your object.</span></span> <span data-ttu-id="10f2d-199">Si elle n’est pas exacte, vous pouvez dessiner vos propres.</span><span class="sxs-lookup"><span data-stu-id="10f2d-199">If it is not accurate, you can draw your own.</span></span> <span data-ttu-id="10f2d-200">Pour cela, en maintenant le clic gauche sur la souris, en faisant glisser la zone sélectionnée pour votre objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-200">This is accomplished by holding left-click on the mouse, and dragging the selection region to encompass your object.</span></span> 

    ![](images/AzureLabs-Lab310-13.png) 

9. <span data-ttu-id="10f2d-201">Après la sélection de votre objet dans l’image, une petite invite vous demandera vous *ajouter les balises Region*.</span><span class="sxs-lookup"><span data-stu-id="10f2d-201">Following the selection of your object within the image, a small prompt will ask for you to *Add Region Tag*.</span></span> <span data-ttu-id="10f2d-202">Sélectionnez votre balise créé précédemment ('Cup', dans l’exemple ci-dessus), ou si vous ajoutez des balises de plus, dans le type et cliquez sur le **+ (plus)** bouton.</span><span class="sxs-lookup"><span data-stu-id="10f2d-202">Select your previously created tag ('Cup', in the above example), or if you are adding more tags, type that in and click the **+ (plus)** button.</span></span>

    ![](images/AzureLabs-Lab310-14.png) 

10. <span data-ttu-id="10f2d-203">Pour marquer l’image suivante, cliquez sur la flèche à droite du panneau, ou fermez le panneau de balise (en cliquant sur le **X** dans l’angle supérieur droit du panneau) puis cliquez sur l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="10f2d-203">To tag the next image, you can click the arrow to the right of the blade, or close the tag blade (by clicking the **X** in the top-right corner of the blade) and then click the next image.</span></span> <span data-ttu-id="10f2d-204">Une fois que vous avez l’image suivante prêt, répétez la même procédure.</span><span class="sxs-lookup"><span data-stu-id="10f2d-204">Once you have the next image ready, repeat the same procedure.</span></span> <span data-ttu-id="10f2d-205">Pour toutes les images que vous avez chargé, jusqu'à ce qu’elles sont marquées pour cela.</span><span class="sxs-lookup"><span data-stu-id="10f2d-205">Do this for all the images you have uploaded, until they are all tagged.</span></span> 

    > [!NOTE]
    >  <span data-ttu-id="10f2d-206">Vous pouvez sélectionner plusieurs objets dans la même image, comme dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10f2d-206">You can select several objects in the same image, like the image below:</span></span> 
    > 
    > ![](images/AzureLabs-Lab310-15.png)

11. <span data-ttu-id="10f2d-207">Une fois que vous avez marqué toutes les, cliquez sur le **avec balises** bouton, sur la gauche de l’écran, pour afficher les images avec balises.</span><span class="sxs-lookup"><span data-stu-id="10f2d-207">Once you have tagged them all, click on the **tagged** button, on the left of the screen, to reveal the tagged images.</span></span> 

    ![](images/AzureLabs-Lab310-16.png)

12. <span data-ttu-id="10f2d-208">Vous êtes maintenant prêt à former votre Service.</span><span class="sxs-lookup"><span data-stu-id="10f2d-208">You are now ready to train your Service.</span></span> <span data-ttu-id="10f2d-209">Cliquez sur le **Train** bouton et la première itération d’entraînement commencera.</span><span class="sxs-lookup"><span data-stu-id="10f2d-209">Click the **Train** button, and the first training iteration will begin.</span></span>

    ![](images/AzureLabs-Lab310-17.png)

    ![](images/AzureLabs-Lab310-18.png)

13. <span data-ttu-id="10f2d-210">Une fois qu’il est créé, vous serez en mesure de voir les deux boutons nommés **par défaut** et **prédiction URL**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-210">Once it is built, you will be able to see two buttons called **Make default** and **Prediction URL**.</span></span> <span data-ttu-id="10f2d-211">Cliquez sur **par défaut** tout d’abord, puis cliquez sur **prédiction URL**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-211">Click on **Make default** first, then click on **Prediction URL**.</span></span>

    ![](images/AzureLabs-Lab310-19.png)

    > [!NOTE] 
    > <span data-ttu-id="10f2d-212">Le point de terminaison qui est fourni à partir de ce problème, selon ce qui a *itération* a été marquée comme valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="10f2d-212">The endpoint which is provided from this, is set to whichever *Iteration* has been marked as default.</span></span> <span data-ttu-id="10f2d-213">Par conséquent, si vous apportez ultérieurement un nouveau *itération* et mettez-le à jour comme valeur par défaut, vous ne devez pas modifier votre code.</span><span class="sxs-lookup"><span data-stu-id="10f2d-213">As such, if you later make a new *Iteration* and update it as default, you will not need to change your code.</span></span>

14. <span data-ttu-id="10f2d-214">Une fois que vous avez cliqué sur **prédiction URL**, ouvrez *le bloc-notes*, puis copiez et collez le **URL** (également appelé votre **prédiction-point de terminaison**) et le **prédiction-clé du Service**, de sorte que vous pouvez les récupérer lorsque vous en avez besoin plus loin dans le code.</span><span class="sxs-lookup"><span data-stu-id="10f2d-214">Once you have clicked on **Prediction URL**, open *Notepad*, and copy and paste the **URL** (also called your **Prediction-Endpoint**) and the **Service Prediction-Key**, so that you can retrieve it when you need it later in the code.</span></span>

    ![](images/AzureLabs-Lab310-20.png)

## <a name="chapter-3---set-up-the-unity-project"></a><span data-ttu-id="10f2d-215">Chapitre 3 - configurer le projet Unity</span><span class="sxs-lookup"><span data-stu-id="10f2d-215">Chapter 3 - Set up the Unity project</span></span>

<span data-ttu-id="10f2d-216">Ce qui suit est un standard configurée pour le développement avec la réalité mixte et par conséquent, est un bon modèle pour d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="10f2d-216">The following is a typical set up for developing with mixed reality, and as such, is a good template for other projects.</span></span>

1.  <span data-ttu-id="10f2d-217">Ouvrez **Unity** et cliquez sur **New**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-217">Open **Unity** and click **New**.</span></span>

    ![](images/AzureLabs-Lab310-21.png)

2.  <span data-ttu-id="10f2d-218">Maintenant, vous devez fournir un nom de projet Unity.</span><span class="sxs-lookup"><span data-stu-id="10f2d-218">You will now need to provide a Unity project name.</span></span> <span data-ttu-id="10f2d-219">Insérer **CustomVisionObjDetection**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-219">Insert **CustomVisionObjDetection**.</span></span> <span data-ttu-id="10f2d-220">Assurez-vous que le type de projet est défini sur **3D**et définissez le **emplacement** à un emplacement approprié pour vous (n’oubliez pas, plus proche de répertoires racine est préférable).</span><span class="sxs-lookup"><span data-stu-id="10f2d-220">Make sure the project type is set to **3D**, and set the **Location** to somewhere appropriate for you (remember, closer to root directories is better).</span></span> <span data-ttu-id="10f2d-221">Ensuite, cliquez sur **créer un projet**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-221">Then, click **Create project**.</span></span>

    ![](images/AzureLabs-Lab310-22.png)

3.  <span data-ttu-id="10f2d-222">Avec Unity ouvert, il est important de la vérification de la valeur par défaut **Script Editor** a la valeur **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-222">With Unity open, it is worth checking the default **Script Editor** is set to **Visual Studio**.</span></span> <span data-ttu-id="10f2d-223">Accédez à **modifier* > *préférences** et à partir de la nouvelle fenêtre, accédez à **outils externes**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-223">Go to **Edit* > *Preferences** and then from the new window, navigate to **External Tools**.</span></span> <span data-ttu-id="10f2d-224">Modification **éditeur de Script externe** à **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-224">Change **External Script Editor** to **Visual Studio**.</span></span> <span data-ttu-id="10f2d-225">Fermer le **préférences** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="10f2d-225">Close the **Preferences** window.</span></span>

    ![](images/AzureLabs-Lab310-23.png)

4.  <span data-ttu-id="10f2d-226">Ensuite, accédez à **fichier > Paramètres de Build** et basculez le **plateforme** à *plateforme Windows universelle*, puis en cliquant sur le **basculer plateforme** bouton.</span><span class="sxs-lookup"><span data-stu-id="10f2d-226">Next, go to **File > Build Settings** and switch the **Platform** to *Universal Windows Platform*, and then clicking on the **Switch Platform** button.</span></span>

    ![](images/AzureLabs-Lab310-24.png)

5.  <span data-ttu-id="10f2d-227">Dans le même **paramètres de Build** fenêtre, vérifiez les éléments suivants sont définis :</span><span class="sxs-lookup"><span data-stu-id="10f2d-227">In the same **Build Settings** window, ensure the following are set:</span></span>

    1.  <span data-ttu-id="10f2d-228">**Équipement cible** a la valeur **HoloLens**</span><span class="sxs-lookup"><span data-stu-id="10f2d-228">**Target Device** is set to **HoloLens**</span></span>        
    2.  <span data-ttu-id="10f2d-229">**Type de build** a la valeur **D3D**</span><span class="sxs-lookup"><span data-stu-id="10f2d-229">**Build Type** is set to **D3D**</span></span>
    3.  <span data-ttu-id="10f2d-230">**Kit de développement logiciel** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="10f2d-230">**SDK** is set to **Latest installed**</span></span>
    4.  <span data-ttu-id="10f2d-231">**Version de Visual Studio** a la valeur **dernière installé**</span><span class="sxs-lookup"><span data-stu-id="10f2d-231">**Visual Studio Version** is set to **Latest installed**</span></span>
    5.  <span data-ttu-id="10f2d-232">**Générez et exécutez** est défini sur **ordinateur Local**</span><span class="sxs-lookup"><span data-stu-id="10f2d-232">**Build and Run** is set to **Local Machine**</span></span>            
    6.  <span data-ttu-id="10f2d-233">Les autres paramètres, dans **paramètres de Build**, doit être conservé comme valeur par défaut pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="10f2d-233">The remaining settings, in **Build Settings**, should be left as default for now.</span></span>

        ![](images/AzureLabs-Lab310-25.png)

6.  <span data-ttu-id="10f2d-234">Dans le même **paramètres de Build** fenêtre, cliquez sur le **paramètres du lecteur** bouton, le panneau de configuration associée s’ouvre dans l’espace où le **inspecteur** se trouve.</span><span class="sxs-lookup"><span data-stu-id="10f2d-234">In the same **Build Settings** window, click on the **Player Settings** button, this will open the related panel in the space where the **Inspector** is located.</span></span>

7. <span data-ttu-id="10f2d-235">Dans ce panneau, quelques paramètres doivent être vérifiées :</span><span class="sxs-lookup"><span data-stu-id="10f2d-235">In this panel, a few settings need to be verified:</span></span>

    1.  <span data-ttu-id="10f2d-236">Dans le **autres paramètres** onglet :</span><span class="sxs-lookup"><span data-stu-id="10f2d-236">In the **Other Settings** tab:</span></span>

        1.  <span data-ttu-id="10f2d-237">**Version du Runtime de script** doit être **expérimental** (.NET 4.6 équivalent), ce qui déclenchera une nécessité de redémarrer l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="10f2d-237">**Scripting Runtime Version** should be **Experimental** (.NET 4.6 Equivalent), which will trigger a need to restart the Editor.</span></span>

        2. <span data-ttu-id="10f2d-238">**Script principal** doit être **.NET**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-238">**Scripting Backend** should be **.NET**.</span></span>

        3. <span data-ttu-id="10f2d-239">**Niveau de compatibilité d’API** doit être **.NET 4.6**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-239">**API Compatibility Level** should be **.NET 4.6**.</span></span>

            ![](images/AzureLabs-Lab310-26.png)

    2.  <span data-ttu-id="10f2d-240">Dans le **paramètres de publication** sous l’onglet sous **fonctionnalités**, vérifiez :</span><span class="sxs-lookup"><span data-stu-id="10f2d-240">Within the **Publishing Settings** tab, under **Capabilities**, check:</span></span>

        1. <span data-ttu-id="10f2d-241">**InternetClient**</span><span class="sxs-lookup"><span data-stu-id="10f2d-241">**InternetClient**</span></span>

        2.  <span data-ttu-id="10f2d-242">**Webcam**</span><span class="sxs-lookup"><span data-stu-id="10f2d-242">**Webcam**</span></span>

        3. <span data-ttu-id="10f2d-243">**SpatialPerception**</span><span class="sxs-lookup"><span data-stu-id="10f2d-243">**SpatialPerception**</span></span>

            <span data-ttu-id="10f2d-244">![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)</span><span class="sxs-lookup"><span data-stu-id="10f2d-244">![](images/AzureLabs-Lab310-27.png) ![](images/AzureLabs-Lab310-28.png)</span></span>

    3.  <span data-ttu-id="10f2d-245">Le panneau de configuration, plus loin dans **XR paramètres** (située sous **paramètres de publication**), graduation **virtuel pris en charge de réalité**, puis assurez-vous que le **mixte Windows Réalité SDK** est ajouté.</span><span class="sxs-lookup"><span data-stu-id="10f2d-245">Further down the panel, in **XR Settings** (found below **Publish Settings**), tick **Virtual Reality Supported**, then make sure the **Windows Mixed Reality SDK** is added.</span></span>

        ![](images/AzureLabs-Lab310-29.png)

8.  <span data-ttu-id="10f2d-246">Dans **paramètres de Build**, *Unity C\# projets* est n’est plus grisée : cochez la case à cocher en regard de cela.</span><span class="sxs-lookup"><span data-stu-id="10f2d-246">Back in **Build Settings**, *Unity C\# Projects* is no longer greyed out: tick the checkbox next to this.</span></span>

9.  <span data-ttu-id="10f2d-247">Fermer le **paramètres de Build** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="10f2d-247">Close the **Build Settings** window.</span></span>

10. <span data-ttu-id="10f2d-248">Dans le **éditeur**, cliquez sur **modifier** > **paramètres du projet** > **graphiques**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-248">In the **Editor**, click on **Edit** > **Project Settings** > **Graphics**.</span></span>

    ![](images/AzureLabs-Lab310-30.png)

11. <span data-ttu-id="10f2d-249">Dans le **panneau Inspecteur** le *paramètres graphiques* seront ouvertes.</span><span class="sxs-lookup"><span data-stu-id="10f2d-249">In the **Inspector Panel** the *Graphics Settings* will be open.</span></span> <span data-ttu-id="10f2d-250">Défiler vers le bas jusqu'à ce que vous voyiez un tableau appelé **incluent toujours les nuanceurs**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-250">Scroll down until you see an array called **Always Include Shaders**.</span></span> <span data-ttu-id="10f2d-251">Ajouter un emplacement en augmentant la **taille** variable d’une unité (dans cet exemple, il avait la valeur 8 pourquoi nous fait il 9).</span><span class="sxs-lookup"><span data-stu-id="10f2d-251">Add a slot by increasing the **Size** variable by one (in this example, it was 8 so we made it 9).</span></span> <span data-ttu-id="10f2d-252">Un nouvel emplacement s’affiche, dans la dernière position du tableau, comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10f2d-252">A new slot will appear, in the last position of the array, as shown below:</span></span>

    ![](images/AzureLabs-Lab310-31.png)

12. <span data-ttu-id="10f2d-253">Dans l’emplacement, cliquez sur le cercle de cible de petite taille en regard de l’emplacement pour ouvrir une liste des nuanceurs.</span><span class="sxs-lookup"><span data-stu-id="10f2d-253">In the slot, click on the small target circle next to the slot to open a list of shaders.</span></span> <span data-ttu-id="10f2d-254">Recherchez le **hérité nuanceurs/Transparent/diffusion** nuanceur et double-cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="10f2d-254">Look for the **Legacy Shaders/Transparent/Diffuse** shader and double-click it.</span></span> 

    ![](images/AzureLabs-Lab310-32.png)

## <a name="chapter-4---importing-the-customvisionobjdetection-unity-package"></a><span data-ttu-id="10f2d-255">Chapitre 4 - Importation du package CustomVisionObjDetection Unity</span><span class="sxs-lookup"><span data-stu-id="10f2d-255">Chapter 4 - Importing the CustomVisionObjDetection Unity package</span></span>

<span data-ttu-id="10f2d-256">Pour ce cours vous sont fournis avec un Package de ressource Unity appelé **Azure-MR-310.unitypackage**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-256">For this course you are provided with a Unity Asset Package called **Azure-MR-310.unitypackage**.</span></span> 

> <span data-ttu-id="10f2d-257">[CONSEIL] Tous les objets pris en charge par Unity, notamment des scènes, peuvent être empaquetés dans un **.unitypackage** de fichiers et exportés / importés dans d’autres projets.</span><span class="sxs-lookup"><span data-stu-id="10f2d-257">[TIP] Any objects supported by Unity, including entire scenes, can be packaged into a **.unitypackage** file, and exported / imported in other projects.</span></span> <span data-ttu-id="10f2d-258">C’est le moyen le plus sûr et plus efficace, pour déplacer des ressources entre différents **projets Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-258">It is the safest, and most efficient, way to move assets between different **Unity projects**.</span></span>

<span data-ttu-id="10f2d-259">Vous pouvez trouver la [package Azure-MR-310 dont vous avez besoin pour télécharger ici](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).</span><span class="sxs-lookup"><span data-stu-id="10f2d-259">You can find the [Azure-MR-310 package that you need to download here](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20310%20-%20Object%20detection/Azure-MR-310.unitypackage).</span></span>

1.  <span data-ttu-id="10f2d-260">Avec le tableau de bord Unity devant vous, cliquez sur **actifs** dans le menu en haut de l’écran, puis cliquez sur **importer un Package > Custom Package**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-260">With the Unity dashboard in front of you, click on **Assets** in the menu at the top of the screen, then click on **Import Package > Custom Package**.</span></span>

    ![](images/AzureLabs-Lab310-33.png)

2.  <span data-ttu-id="10f2d-261">Utilisez le sélecteur de fichiers pour sélectionner le **Azure-MR-310.unitypackage** du package et cliquez sur **Open**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-261">Use the file picker to select the **Azure-MR-310.unitypackage** package and click **Open**.</span></span> <span data-ttu-id="10f2d-262">Une liste des composants de cette ressource s’affichera pour vous.</span><span class="sxs-lookup"><span data-stu-id="10f2d-262">A list of components for this asset will be displayed to you.</span></span> <span data-ttu-id="10f2d-263">Confirmez l’importation en cliquant sur le **importer** bouton.</span><span class="sxs-lookup"><span data-stu-id="10f2d-263">Confirm the import by clicking the **Import** button.</span></span>

    ![](images/AzureLabs-Lab310-34.png)

3.  <span data-ttu-id="10f2d-264">Une fois l’importation terminée, vous remarquerez que les dossiers à partir du package ont désormais été ajoutées à votre **actifs** dossier.</span><span class="sxs-lookup"><span data-stu-id="10f2d-264">Once it has finished importing, you will notice that folders from the package have now been added to your **Assets** folder.</span></span> <span data-ttu-id="10f2d-265">Ce type de structure de dossiers est généralement utilisé pour un projet Unity.</span><span class="sxs-lookup"><span data-stu-id="10f2d-265">This kind of folder structure is typical for a Unity project.</span></span>

    ![](images/AzureLabs-Lab310-35.png)

    1.  <span data-ttu-id="10f2d-266">Le **matériaux** dossier contient le matériel utilisé par le **curseur les regards**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-266">The **Materials** folder contains the material used by the **Gaze Cursor**.</span></span> 

    2.  <span data-ttu-id="10f2d-267">Le **plug-ins** dossier contient la DLL Newtonsoft utilisé par le code pour désérialiser la réponse du Service web.</span><span class="sxs-lookup"><span data-stu-id="10f2d-267">The **Plugins** folder contains the Newtonsoft DLL used by the code to deserialize the Service web response.</span></span> <span data-ttu-id="10f2d-268">Les deux (2) différentes versions contenues dans le dossier et un sous-dossier, sont nécessaires pour que la bibliothèque à utiliser et généré par l’éditeur Unity et de la build UWP.</span><span class="sxs-lookup"><span data-stu-id="10f2d-268">The two (2) different versions contained in the folder, and sub-folder, are necessary to allow the library to be used and built by both the Unity Editor and the UWP build.</span></span> 

    3.  <span data-ttu-id="10f2d-269">Le **Prefabs** dossier contient les prefabs contenues dans la scène.</span><span class="sxs-lookup"><span data-stu-id="10f2d-269">The **Prefabs** folder contains the prefabs contained in the scene.</span></span> <span data-ttu-id="10f2d-270">Ce sont :</span><span class="sxs-lookup"><span data-stu-id="10f2d-270">Those are:</span></span>

        1.  <span data-ttu-id="10f2d-271">Le **GazeCursor**, le curseur utilisé dans l’application.</span><span class="sxs-lookup"><span data-stu-id="10f2d-271">The **GazeCursor**, the cursor used in the application.</span></span> <span data-ttu-id="10f2d-272">Fonctionne avec le préfabriqué SpatialMapping pour pouvoir être placé dans la scène au-dessus des objets physiques.</span><span class="sxs-lookup"><span data-stu-id="10f2d-272">Will work together with the SpatialMapping prefab to be able to be placed in the scene on top of physical objects.</span></span>
        2.  <span data-ttu-id="10f2d-273">Le **étiquette**, qui est l’objet d’interface utilisateur permettant d’afficher la balise object dans la scène lorsque nécessaire.</span><span class="sxs-lookup"><span data-stu-id="10f2d-273">The **Label**, which is the UI object used to display the object tag in the scene when required.</span></span>
        3.  <span data-ttu-id="10f2d-274">Le **SpatialMapping**, qui est l’objet qui permet à l’application à utiliser crée une carte virtuelle, à l’aide de suivi spatial du Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="10f2d-274">The **SpatialMapping**, which is the object that enables the application to use create a virtual map, using the Microsoft HoloLens' spatial tracking.</span></span>

    4.  <span data-ttu-id="10f2d-275">Le **scènes** dossier qui contient actuellement la scène prédéfinie pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="10f2d-275">The **Scenes** folder which currently contains the pre-built scene for this course.</span></span>

4.  <span data-ttu-id="10f2d-276">Ouvrir le **scènes** dossier, dans le **panneau projet**et double-cliquez sur le **ObjDetectionScene**, pour charger la scène que vous allez utiliser pour ce cours.</span><span class="sxs-lookup"><span data-stu-id="10f2d-276">Open the **Scenes** folder, in the **Project Panel**, and double-click on the **ObjDetectionScene**, to load the scene that you will use for this course.</span></span>

    ![](images/AzureLabs-Lab310-36.png)

    > [!NOTE] 
    >  <span data-ttu-id="10f2d-277">**Aucun code n’est inclus**, vous allez écrire le code en suivant ce cours.</span><span class="sxs-lookup"><span data-stu-id="10f2d-277">**No code is included**, you will write the code by following this course.</span></span>

## <a name="chapter-5---create-the-customvisionanalyser-class"></a><span data-ttu-id="10f2d-278">Chapitre 5 : créer la classe CustomVisionAnalyser.</span><span class="sxs-lookup"><span data-stu-id="10f2d-278">Chapter 5 - Create the CustomVisionAnalyser class.</span></span>

<span data-ttu-id="10f2d-279">À ce stade, vous êtes prêt à écrire du code.</span><span class="sxs-lookup"><span data-stu-id="10f2d-279">At this point you are ready to write some code.</span></span> <span data-ttu-id="10f2d-280">Vous allez commencer avec le **CustomVisionAnalyser** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-280">You will begin with the **CustomVisionAnalyser** class.</span></span>

> [!NOTE]
> <span data-ttu-id="10f2d-281">Les appels à la **Service Vision personnalisée**, effectuée dans le code indiqué ci-dessous, sont effectuées à l’aide de la **API REST de Vision personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-281">The calls to the **Custom Vision Service**, made in the code shown below, are made using the **Custom Vision REST API**.</span></span> <span data-ttu-id="10f2d-282">Via l’utilisant, vous verrez comment implémenter et utiliser cette API (utile pour comprendre comment implémenter quelque chose de similaire sur votre propre).</span><span class="sxs-lookup"><span data-stu-id="10f2d-282">Through using this, you will see how to implement and make use of this API (useful for understanding how to implement something similar on your own).</span></span> <span data-ttu-id="10f2d-283">Sachez que Microsoft propose un **Custom Vision SDK** qui peut également être utilisé pour effectuer des appels au Service.</span><span class="sxs-lookup"><span data-stu-id="10f2d-283">Be aware, that Microsoft offers a **Custom Vision SDK** that can also be used to make calls to the Service.</span></span> <span data-ttu-id="10f2d-284">Pour plus d’informations, visitez le [article du Kit de développement logiciel Custom Vision](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).</span><span class="sxs-lookup"><span data-stu-id="10f2d-284">For more information visit the [Custom Vision SDK article](https://github.com/Microsoft/Cognitive-CustomVision-Windows/).</span></span>

<span data-ttu-id="10f2d-285">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="10f2d-285">This class is responsible for:</span></span>

- <span data-ttu-id="10f2d-286">Chargement de la dernière image capturée sous la forme d’un tableau d’octets.</span><span class="sxs-lookup"><span data-stu-id="10f2d-286">Loading the latest image captured as an array of bytes.</span></span>

- <span data-ttu-id="10f2d-287">Envoyer le tableau d’octets à votre Azure **Service Vision personnalisée** instance pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="10f2d-287">Sending the byte array to your Azure **Custom Vision Service** instance for analysis.</span></span>

- <span data-ttu-id="10f2d-288">Recevoir une réponse sous forme de chaîne JSON.</span><span class="sxs-lookup"><span data-stu-id="10f2d-288">Receiving the response as a JSON string.</span></span>

- <span data-ttu-id="10f2d-289">La désérialisation de la réponse et en passant résultant **prédiction** à la **SceneOrganiser** (classe), qui se chargera de la façon dont la réponse doit être affichée.</span><span class="sxs-lookup"><span data-stu-id="10f2d-289">Deserializing the response and passing the resulting **Prediction** to the **SceneOrganiser** class, which will take care of how the response should be displayed.</span></span>

<span data-ttu-id="10f2d-290">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-290">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-291">Avec le bouton droit dans le **dossier composants**, situé dans le **panneau projet**, puis cliquez sur **créer** > **dossier**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-291">Right-click in the **Asset Folder**, located in the **Project Panel**, then click **Create** > **Folder**.</span></span> <span data-ttu-id="10f2d-292">Appelez le dossier **Scripts**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-292">Call the folder **Scripts**.</span></span>

    ![](images/AzureLabs-Lab310-37.png)

2.  <span data-ttu-id="10f2d-293">Double-cliquez sur le dossier nouvellement créé, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="10f2d-293">Double-click on the newly created folder, to open it.</span></span>

3.  <span data-ttu-id="10f2d-294">Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-294">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-295">Nommez le script **CustomVisionAnalyser.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-295">Name the script **CustomVisionAnalyser.**</span></span>

4.  <span data-ttu-id="10f2d-296">Double-cliquez sur le nouveau **CustomVisionAnalyser** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-296">Double-click on the new **CustomVisionAnalyser** script to open it with **Visual Studio.**</span></span>

5.  <span data-ttu-id="10f2d-297">Vérifiez que vous disposez des espaces de noms suivants référencé au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="10f2d-297">Make sure you have the following namespaces referenced at the top of the file:</span></span>

    ```csharp
    using Newtonsoft.Json;
    using System.Collections;
    using System.IO;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

6.  <span data-ttu-id="10f2d-298">Dans le **CustomVisionAnalyser** de classe, ajoutez les variables suivantes :</span><span class="sxs-lookup"><span data-stu-id="10f2d-298">In the **CustomVisionAnalyser** class, add the following variables:</span></span>

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
    > <span data-ttu-id="10f2d-299">Assurez-vous que vous insérez votre **prédiction-clé du Service** dans le **predictionKey** variable et votre **prédiction-point de terminaison** dans le **predictionEndpoint**  variable.</span><span class="sxs-lookup"><span data-stu-id="10f2d-299">Make sure you insert your **Service Prediction-Key** into the **predictionKey** variable and your **Prediction-Endpoint** into the **predictionEndpoint** variable.</span></span> <span data-ttu-id="10f2d-300">Vous avez copié à [le bloc-notes précédemment, dans le chapitre 2, l’étape 14](#chapter-2---training-your-custom-vision-project).</span><span class="sxs-lookup"><span data-stu-id="10f2d-300">You copied these to [Notepad earlier, in Chapter 2, Step 14](#chapter-2---training-your-custom-vision-project).</span></span>

7.  <span data-ttu-id="10f2d-301">Code pour **Awake()** doit maintenant être ajouté pour initialiser la variable d’Instance :</span><span class="sxs-lookup"><span data-stu-id="10f2d-301">Code for **Awake()** now needs to be added to initialize the Instance variable:</span></span>

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

8.  <span data-ttu-id="10f2d-302">Ajouter la coroutine (avec la méthode statique **GetImageAsByteArray()** méthode en dessous), qui obtient les résultats de l’analyse de l’image capturée par le **ImageCapture** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-302">Add the coroutine (with the static **GetImageAsByteArray()** method below it), which will obtain the results of the analysis of the image, captured by the **ImageCapture** class.</span></span>

    > [!NOTE]
    > <span data-ttu-id="10f2d-303">Dans le **AnalyseImageCapture** coroutine, il existe un appel à la **SceneOrganiser** classe que vous êtes encore à créer.</span><span class="sxs-lookup"><span data-stu-id="10f2d-303">In the **AnalyseImageCapture** coroutine, there is a call to the **SceneOrganiser** class that you are yet to create.</span></span> <span data-ttu-id="10f2d-304">Par conséquent, **laisser les lignes commentées pour l’instant**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-304">Therefore, **leave those lines commented for now**.</span></span>

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

9. <span data-ttu-id="10f2d-305">Supprimer le **Start()** et **Update()** méthodes, car ils ne seront pas utilisés.</span><span class="sxs-lookup"><span data-stu-id="10f2d-305">Delete the **Start()** and **Update()** methods, as they will not be used.</span></span> 

10.  <span data-ttu-id="10f2d-306">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-306">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10f2d-307">Comme mentionné précédemment, ne vous inquiétez pas sur le code qui peut sembler avoir une erreur, comme vous fournit des classes plus rapidement, ce qui résoudra ces.</span><span class="sxs-lookup"><span data-stu-id="10f2d-307">As mentioned earlier, do not worry about code which might appear to have an error, as you will provide further classes soon, which will fix these.</span></span>

## <a name="chapter-6---create-the-customvisionobjects-class"></a><span data-ttu-id="10f2d-308">Chapitre 6 : créer la classe CustomVisionObjects</span><span class="sxs-lookup"><span data-stu-id="10f2d-308">Chapter 6 - Create the CustomVisionObjects class</span></span>

<span data-ttu-id="10f2d-309">La classe que vous allez créer est maintenant le **CustomVisionObjects** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-309">The class you will create now is the **CustomVisionObjects** class.</span></span>

<span data-ttu-id="10f2d-310">Ce script contient un nombre d’objets utilisés par d’autres classes pour sérialiser et désérialiser les appels effectués vers le Service Vision personnalisée.</span><span class="sxs-lookup"><span data-stu-id="10f2d-310">This script contains a number of objects used by other classes to serialize and deserialize the calls made to the Custom Vision Service.</span></span>

<span data-ttu-id="10f2d-311">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-311">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-312">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-312">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-313">Appeler le script **CustomVisionObjects.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-313">Call the script **CustomVisionObjects.**</span></span>

2.  <span data-ttu-id="10f2d-314">Double-cliquez sur le nouveau **CustomVisionObjects** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-314">Double-click on the new **CustomVisionObjects** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="10f2d-315">Vérifiez que vous disposez des espaces de noms suivants référencé au début du fichier :</span><span class="sxs-lookup"><span data-stu-id="10f2d-315">Make sure you have the following namespaces referenced at the top of the file:</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using UnityEngine;
    using UnityEngine.Networking;
    ```

4.  <span data-ttu-id="10f2d-316">Supprimer le **Start()** et **Update()** méthodes à l’intérieur de la **CustomVisionObjects** classe, cette classe doit maintenant être vide.</span><span class="sxs-lookup"><span data-stu-id="10f2d-316">Delete the **Start()** and **Update()** methods inside the **CustomVisionObjects** class, this class should now be empty.</span></span>

    > [!WARNING]
    > <span data-ttu-id="10f2d-317">Il est important que vous suivez la prochaine instruction avec précaution.</span><span class="sxs-lookup"><span data-stu-id="10f2d-317">It is important you follow the next instruction carefully.</span></span> <span data-ttu-id="10f2d-318">Si vous placez les déclarations de classe nouvelle à l’intérieur de la **CustomVisionObjects** (classe), vous obtiendrez des erreurs de compilation [chapitre 10](#chapter-10---create-the-imagecapture-class), indiquant que **AnalysisRootObject** et  **BoundingBox** sont introuvables.</span><span class="sxs-lookup"><span data-stu-id="10f2d-318">If you put the new class declarations inside the **CustomVisionObjects** class, you will get compile errors in [chapter 10](#chapter-10---create-the-imagecapture-class), stating that **AnalysisRootObject** and **BoundingBox** are not found.</span></span>

5.  <span data-ttu-id="10f2d-319">Ajoutez les classes suivantes *en dehors de* le **CustomVisionObjects** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-319">Add the following classes *outside* the **CustomVisionObjects** class.</span></span> <span data-ttu-id="10f2d-320">Ces objets sont utilisés par le **Newtonsoft** bibliothèque pour sérialiser et désérialiser les données de réponse :</span><span class="sxs-lookup"><span data-stu-id="10f2d-320">These objects are used by the **Newtonsoft** library to serialize and deserialize the response data:</span></span>

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

6.  <span data-ttu-id="10f2d-321">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-321">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-7---create-the-spatialmapping-class"></a><span data-ttu-id="10f2d-322">Chapitre 7 - créer la classe SpatialMapping</span><span class="sxs-lookup"><span data-stu-id="10f2d-322">Chapter 7 - Create the SpatialMapping class</span></span>

<span data-ttu-id="10f2d-323">Cette classe définira le **Collider de mappage Spatial** dans la scène. ainsi, pour être en mesure de détecter les collisions entre des objets virtuels et des objets réels.</span><span class="sxs-lookup"><span data-stu-id="10f2d-323">This class will set the **Spatial Mapping Collider** in the scene so to be able to detect collisions between virtual objects and real objects.</span></span>

<span data-ttu-id="10f2d-324">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-324">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-325">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-325">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-326">Appeler le script **SpatialMapping.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-326">Call the script **SpatialMapping.**</span></span>

2.  <span data-ttu-id="10f2d-327">Double-cliquez sur le nouveau **SpatialMapping** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-327">Double-click on the new **SpatialMapping** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="10f2d-328">Vérifiez que vous disposez des espaces de noms suivants mentionnés ci-dessus le **SpatialMapping** classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-328">Make sure you have the following namespaces referenced above the **SpatialMapping** class:</span></span>

    ```csharp
    using UnityEngine;
    using UnityEngine.XR.WSA;
    ```

4.  <span data-ttu-id="10f2d-329">Ensuite, ajoutez les variables suivantes à l’intérieur de la **SpatialMapping** classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="10f2d-329">Then, add the following variables inside the **SpatialMapping** class, above the **Start()** method:</span></span>

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

5.  <span data-ttu-id="10f2d-330">Ajouter le **Awake()** et **Start()**:</span><span class="sxs-lookup"><span data-stu-id="10f2d-330">Add the **Awake()** and **Start()**:</span></span>

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

6.  <span data-ttu-id="10f2d-331">Supprimer le **Update()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="10f2d-331">Delete the **Update()** method.</span></span>

7.  <span data-ttu-id="10f2d-332">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-332">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>


## <a name="chapter-8---create-the-gazecursor-class"></a><span data-ttu-id="10f2d-333">Chapitre 8 - créer la classe GazeCursor</span><span class="sxs-lookup"><span data-stu-id="10f2d-333">Chapter 8 - Create the GazeCursor class</span></span>

<span data-ttu-id="10f2d-334">Cette classe est responsable de la configuration du curseur à l’emplacement approprié dans l’espace réel, en utilisant le **SpatialMappingCollider**, créé dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="10f2d-334">This class is responsible for setting up the cursor in the correct location in real space, by making use of the **SpatialMappingCollider**, created in the previous chapter.</span></span>

<span data-ttu-id="10f2d-335">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-335">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-336">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-336">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-337">Appeler le script **GazeCursor**</span><span class="sxs-lookup"><span data-stu-id="10f2d-337">Call the script **GazeCursor**</span></span>

2.  <span data-ttu-id="10f2d-338">Double-cliquez sur le nouveau **GazeCursor** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-338">Double-click on the new **GazeCursor** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="10f2d-339">Vérifiez que vous disposez de l’espace de noms suivant référencé ci-dessus le **GazeCursor** classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-339">Make sure you have the following namespace referenced above the **GazeCursor** class:</span></span>

    ```csharp
    using UnityEngine;
    ```

4.  <span data-ttu-id="10f2d-340">Puis ajoutez la variable suivante à l’intérieur de la **GazeCursor** de classe, au-dessus du **Start()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="10f2d-340">Then add the following variable inside the **GazeCursor** class, above the **Start()** method.</span></span> 

    ```csharp
        /// <summary>
        /// The cursor (this object) mesh renderer
        /// </summary>
        private MeshRenderer meshRenderer;
    ```

5.  <span data-ttu-id="10f2d-341">Mise à jour le **Start()** méthode avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="10f2d-341">Update the **Start()** method with the following code:</span></span>

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

6.  <span data-ttu-id="10f2d-342">Mise à jour le **Update()** méthode avec le code suivant :</span><span class="sxs-lookup"><span data-stu-id="10f2d-342">Update the **Update()** method with the following code:</span></span>

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
    > <span data-ttu-id="10f2d-343">Ne vous inquiétez pas sur l’erreur pour le **SceneOrganiser** classe introuvable, vous allez le créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="10f2d-343">Do not worry about the error for the **SceneOrganiser** class not being found, you will create it in the next chapter.</span></span>

7. <span data-ttu-id="10f2d-344">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-344">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-9---create-the-sceneorganiser-class"></a><span data-ttu-id="10f2d-345">Chapitre 9 - créer la classe SceneOrganiser</span><span class="sxs-lookup"><span data-stu-id="10f2d-345">Chapter 9 - Create the SceneOrganiser class</span></span>

<span data-ttu-id="10f2d-346">Cette classe sera :</span><span class="sxs-lookup"><span data-stu-id="10f2d-346">This class will:</span></span>

-   <span data-ttu-id="10f2d-347">Configurer le *Main Camera* en joignant les composants appropriés à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="10f2d-347">Set up the *Main Camera* by attaching the appropriate components to it.</span></span>

-   <span data-ttu-id="10f2d-348">Lorsqu’un objet est détecté, il sera responsable du calcul de sa position dans le monde réel et place un **étiquette** près d’avec le bon **nom de balise**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-348">When an object is detected, it will be responsible for calculating its position in the real world and place a **Tag Label** near it with the appropriate **Tag Name**.</span></span>    

<span data-ttu-id="10f2d-349">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-349">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-350">Avec le bouton droit à l’intérieur de la **Scripts** dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-350">Right-click inside the **Scripts** folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-351">Nommez le script **SceneOrganiser**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-351">Name the script **SceneOrganiser**.</span></span>

2.  <span data-ttu-id="10f2d-352">Double-cliquez sur le nouveau **SceneOrganiser** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-352">Double-click on the new **SceneOrganiser** script to open it with **Visual Studio.**</span></span>

3.  <span data-ttu-id="10f2d-353">Vérifiez que vous disposez des espaces de noms suivants mentionnés ci-dessus le **SceneOrganiser** classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-353">Make sure you have the following namespaces referenced above the **SceneOrganiser** class:</span></span>

    ```csharp
    using System.Collections.Generic;
    using System.Linq;
    using UnityEngine;
    ```

4.  <span data-ttu-id="10f2d-354">Puis ajoutez les variables suivantes à l’intérieur de la **SceneOrganiser** classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="10f2d-354">Then add the following variables inside the **SceneOrganiser** class, above the **Start()** method:</span></span>

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

5.  <span data-ttu-id="10f2d-355">Supprimer le **Start()** et **Update()** méthodes.</span><span class="sxs-lookup"><span data-stu-id="10f2d-355">Delete the **Start()** and **Update()** methods.</span></span>

6.  <span data-ttu-id="10f2d-356">Sous les variables, ajoutez le **Awake()** (méthode), qui initialisent la classe et configurer la scène.</span><span class="sxs-lookup"><span data-stu-id="10f2d-356">Underneath the variables, add the **Awake()** method, which will initialize the class and set up the scene.</span></span>

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

7.  <span data-ttu-id="10f2d-357">Ajouter le **PlaceAnalysisLabel()** (méthode), qui sera *instancier* l’étiquette dans la scène (qui est à ce stade invisible à l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="10f2d-357">Add the **PlaceAnalysisLabel()** method, which will *Instantiate* the label in the scene (which at this point is invisible to the user).</span></span> <span data-ttu-id="10f2d-358">Il place également les quatre cœurs (également invisibles) où l’image est placée et se chevauche avec le monde réel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-358">It also places the quad (also invisible) where the image is placed, and overlaps with the real world.</span></span> <span data-ttu-id="10f2d-359">Ceci est important, car les coordonnées de la zone est récupéré à partir du Service après l’analyse sont remonter dans cette quadruple déterminé l’emplacement approximatif de l’objet dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-359">This is important because the box coordinates retrieved from the Service after analysis are traced back into this quad to determined the approximate location of the object in the real world.</span></span> 

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

8.  <span data-ttu-id="10f2d-360">Ajouter le **FinaliseLabel()** (méthode).</span><span class="sxs-lookup"><span data-stu-id="10f2d-360">Add the **FinaliseLabel()** method.</span></span> <span data-ttu-id="10f2d-361">Il est chargé de :</span><span class="sxs-lookup"><span data-stu-id="10f2d-361">It is responsible for:</span></span>

    *   <span data-ttu-id="10f2d-362">Définition de la *étiquette* texte avec le *balise* de la prédiction en toute confiance le plus élevé.</span><span class="sxs-lookup"><span data-stu-id="10f2d-362">Setting the *Label* text with the *Tag* of the Prediction with the highest confidence.</span></span>
    *   <span data-ttu-id="10f2d-363">Le calcul de l’appel le *le rectangle englobant* sur l’objet processeur quadruple, positionné précédemment et la placer l’étiquette dans la scène.</span><span class="sxs-lookup"><span data-stu-id="10f2d-363">Calling the calculation of the *Bounding Box* on the quad object, positioned previously, and placing the label in the scene.</span></span>
    *   <span data-ttu-id="10f2d-364">Ajustement de la profondeur de l’étiquette à l’aide d’un Raycast vers le *le rectangle englobant*, qui doit entrer en conflit par rapport à l’objet dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-364">Adjusting the label depth by using a Raycast towards the *Bounding Box*, which should collide against the object in the real world.</span></span>
    * <span data-ttu-id="10f2d-365">Réinitialiser le processus de capture pour autoriser l’utilisateur à capturer une autre image.</span><span class="sxs-lookup"><span data-stu-id="10f2d-365">Resetting the capture process to allow the user to capture another image.</span></span>

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

9.  <span data-ttu-id="10f2d-366">Ajouter le **CalculateBoundingBoxPosition()** (méthode), qui héberge un nombre de calculs nécessaires pour traduire le *le rectangle englobant* coordonnées extraites du Service et les recréer proportionnellement sur les quatre cœurs.</span><span class="sxs-lookup"><span data-stu-id="10f2d-366">Add the **CalculateBoundingBoxPosition()** method, which hosts a number of calculations necessary to translate the *Bounding Box* coordinates retrieved from the Service and recreate them proportionally on the quad.</span></span>

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

10. <span data-ttu-id="10f2d-367">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-367">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="10f2d-368">Avant de continuer, ouvrez le **CustomVisionAnalyser** (classe) et dans le **AnalyseLastImageCaptured()** (méthode), *Décommentez* les lignes suivantes :</span><span class="sxs-lookup"><span data-stu-id="10f2d-368">Before you continue, open the **CustomVisionAnalyser** class, and within the **AnalyseLastImageCaptured()** method, *uncomment* the following lines:</span></span>
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
> <span data-ttu-id="10f2d-369">Ne vous inquiétez pas sur le **ImageCapture** classe message « est introuvable », vous allez le créer dans le chapitre suivant.</span><span class="sxs-lookup"><span data-stu-id="10f2d-369">Do not worry about the **ImageCapture** class 'could not be found' message, you will create it in the next chapter.</span></span>


## <a name="chapter-10---create-the-imagecapture-class"></a><span data-ttu-id="10f2d-370">Chapitre 10 - créer la classe ImageCapture</span><span class="sxs-lookup"><span data-stu-id="10f2d-370">Chapter 10 - Create the ImageCapture class</span></span>

<span data-ttu-id="10f2d-371">La classe suivante, vous allez créer est la **ImageCapture** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-371">The next class you are going to create is the **ImageCapture** class.</span></span>

<span data-ttu-id="10f2d-372">Cette classe est chargée de :</span><span class="sxs-lookup"><span data-stu-id="10f2d-372">This class is responsible for:</span></span>

*   <span data-ttu-id="10f2d-373">Capture d’une image à l’aide de l’appareil photo HoloLens et en le stockant dans le *application* dossier.</span><span class="sxs-lookup"><span data-stu-id="10f2d-373">Capturing an image using the HoloLens camera and storing it in the *App* folder.</span></span>
*   <span data-ttu-id="10f2d-374">Gestion des *appuyez sur* mouvements de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="10f2d-374">Handling *Tap* gestures from the user.</span></span>

<span data-ttu-id="10f2d-375">Pour créer cette classe :</span><span class="sxs-lookup"><span data-stu-id="10f2d-375">To create this class:</span></span>

1.  <span data-ttu-id="10f2d-376">Accédez à la **Scripts** dossier que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="10f2d-376">Go to the **Scripts** folder you created previously.</span></span>

2.  <span data-ttu-id="10f2d-377">Avec le bouton droit dans le dossier, puis cliquez sur **créer** > **C\# Script**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-377">Right-click inside the folder, then click **Create** > **C\# Script**.</span></span> <span data-ttu-id="10f2d-378">Nommez le script **ImageCapture**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-378">Name the script **ImageCapture**.</span></span>

3.  <span data-ttu-id="10f2d-379">Double-cliquez sur le nouveau **ImageCapture** script pour l’ouvrir avec **Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="10f2d-379">Double-click on the new **ImageCapture** script to open it with **Visual Studio.**</span></span>

4.  <span data-ttu-id="10f2d-380">Remplacez les espaces de noms en haut du fichier avec les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="10f2d-380">Replace the namespaces at the top of the file with the following:</span></span>

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using UnityEngine;
    using UnityEngine.XR.WSA.Input;
    using UnityEngine.XR.WSA.WebCam;
    ```

5.  <span data-ttu-id="10f2d-381">Puis ajoutez les variables suivantes à l’intérieur de la **ImageCapture** classe ci-dessus le **Start()** méthode :</span><span class="sxs-lookup"><span data-stu-id="10f2d-381">Then add the following variables inside the **ImageCapture** class, above the **Start()** method:</span></span>

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

6.  <span data-ttu-id="10f2d-382">Code pour **Awake()** et **Start()** méthodes doit maintenant être ajouté :</span><span class="sxs-lookup"><span data-stu-id="10f2d-382">Code for **Awake()** and **Start()** methods now needs to be added:</span></span>

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

7.  <span data-ttu-id="10f2d-383">Implémenter un gestionnaire qui sera appelé lorsqu’une action d’appuyer se produit :</span><span class="sxs-lookup"><span data-stu-id="10f2d-383">Implement a handler that will be called when a Tap gesture occurs:</span></span>

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
    > <span data-ttu-id="10f2d-384">Lorsque le curseur se trouve **vert**, cela signifie que l’appareil photo est disponible pour la prise de l’image.</span><span class="sxs-lookup"><span data-stu-id="10f2d-384">When the cursor is **green**, it means the camera is available to take the image.</span></span> <span data-ttu-id="10f2d-385">Lorsque le curseur se trouve **rouge**, cela signifie que l’appareil photo est occupé.</span><span class="sxs-lookup"><span data-stu-id="10f2d-385">When the cursor is **red**, it means the camera is busy.</span></span>

8.  <span data-ttu-id="10f2d-386">Ajoutez la méthode que l’application utilise pour démarrer le processus de capture d’image et de stocker l’image :</span><span class="sxs-lookup"><span data-stu-id="10f2d-386">Add the method that the application uses to start the image capture process and store the image:</span></span>

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

9.  <span data-ttu-id="10f2d-387">Ajoutez les gestionnaires qui seront appelées lorsque la photo a été capturée et quand il est prêt à être analysés.</span><span class="sxs-lookup"><span data-stu-id="10f2d-387">Add the handlers that will be called when the photo has been captured and for when it is ready to be analyzed.</span></span> <span data-ttu-id="10f2d-388">Le résultat est ensuite transmis à la **CustomVisionAnalyser** pour l’analyse.</span><span class="sxs-lookup"><span data-stu-id="10f2d-388">The result is then passed to the **CustomVisionAnalyser** for analysis.</span></span>

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

10. <span data-ttu-id="10f2d-389">Veillez à enregistrer vos modifications dans **Visual Studio**, avant de retourner à **Unity**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-389">Be sure to save your changes in **Visual Studio**, before returning to **Unity**.</span></span>

## <a name="chapter-11---setting-up-the-scripts-in-the-scene"></a><span data-ttu-id="10f2d-390">Chapitre 11 - configurer les scripts dans la scène</span><span class="sxs-lookup"><span data-stu-id="10f2d-390">Chapter 11 - Setting up the scripts in the scene</span></span>

<span data-ttu-id="10f2d-391">Maintenant que vous avez écrit tout le code nécessaire pour ce projet, est le temps pour configurer les scripts dans la scène et sur les prefabs, pour qu’ils se comportent correctement.</span><span class="sxs-lookup"><span data-stu-id="10f2d-391">Now that you have written all of the code necessary for this project, is time to set up the scripts in the scene, and on the prefabs, for them to behave correctly.</span></span>

1.  <span data-ttu-id="10f2d-392">Dans le **éditeur Unity**, dans le **hiérarchie panneau**, sélectionnez le **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-392">Within the **Unity Editor**, in the **Hierarchy Panel**, select the **Main Camera**.</span></span>
2.  <span data-ttu-id="10f2d-393">Dans le **panneau Inspecteur**, avec le **Main Camera** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **SceneOrganiser** script et Double-cliquez sur pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="10f2d-393">In the **Inspector Panel**, with the **Main Camera** selected, click on **Add Component**, then search for **SceneOrganiser** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-38.png)

3.  <span data-ttu-id="10f2d-394">Dans le **panneau projet**, ouvrez le **dossier Prefabs**, faites glisser le **étiquette** prefab dans le *étiquette* zone, d’entrée cible de référence vide dans le **SceneOrganiser** script que vous venez d’ajouter à la *Main Camera*, comme illustré dans l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="10f2d-394">In the **Project Panel**, open the **Prefabs folder**, drag the **Label** prefab into the *Label* empty reference target input area, in the **SceneOrganiser** script that you have just added to the *Main Camera*, as shown in the image below:</span></span>

    ![](images/AzureLabs-Lab310-39.png)

4.  <span data-ttu-id="10f2d-395">Dans le **hiérarchie panneau**, sélectionnez le **GazeCursor** enfant de la **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-395">In the **Hierarchy Panel**, select the **GazeCursor** child of the **Main Camera**.</span></span>
5.  <span data-ttu-id="10f2d-396">Dans le **panneau Inspecteur**, avec le **GazeCursor** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **GazeCursor** script et Double-cliquez sur pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="10f2d-396">In the **Inspector Panel**, with the **GazeCursor** selected, click on **Add Component**, then search for **GazeCursor** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-40.png)

6.  <span data-ttu-id="10f2d-397">Là encore, dans le **hiérarchie panneau**, sélectionnez le **SpatialMapping** enfant de la **Main Camera**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-397">Again, in the **Hierarchy Panel**, select the **SpatialMapping** child of the **Main Camera**.</span></span>
7.  <span data-ttu-id="10f2d-398">Dans le **panneau Inspecteur**, avec le **SpatialMapping** sélectionné, cliquez sur **ajouter un composant**, puis recherchez **SpatialMapping** script et le double-clic, pour l’ajouter.</span><span class="sxs-lookup"><span data-stu-id="10f2d-398">In the **Inspector Panel**, with the **SpatialMapping** selected, click on **Add Component**, then search for **SpatialMapping** script and double-click, to add it.</span></span>

    ![](images/AzureLabs-Lab310-41.png)

<span data-ttu-id="10f2d-399">Les scripts restants que vous n’ont pas jeu est ajouté par le code dans le **SceneOrganiser** script, pendant l’exécution.</span><span class="sxs-lookup"><span data-stu-id="10f2d-399">The remaining scripts thats you have not set will be added by the code in the **SceneOrganiser** script, during runtime.</span></span>

## <a name="chapter-12---before-building"></a><span data-ttu-id="10f2d-400">Chapitre 12 - avant la génération</span><span class="sxs-lookup"><span data-stu-id="10f2d-400">Chapter 12 - Before building</span></span>

<span data-ttu-id="10f2d-401">Pour effectuer une analyse minutieuse de votre application vous en aurez besoin pour effectuer un chargement indépendant sur votre Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="10f2d-401">To perform a thorough test of your application you will need to sideload it onto your Microsoft HoloLens.</span></span>

<span data-ttu-id="10f2d-402">Avant de procéder, assurez-vous que :</span><span class="sxs-lookup"><span data-stu-id="10f2d-402">Before you do, ensure that:</span></span>

-  <span data-ttu-id="10f2d-403">Tous les paramètres mentionnés dans le [chapitre 3](#chapter-3---set-up-the-unity-project) sont correctement définies.</span><span class="sxs-lookup"><span data-stu-id="10f2d-403">All the settings mentioned in the [Chapter 3](#chapter-3---set-up-the-unity-project) are set correctly.</span></span>
- <span data-ttu-id="10f2d-404">Le script **SceneOrganiser** est attaché à la **Main Camera** objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-404">The script **SceneOrganiser** is attached to the **Main Camera** object.</span></span>
- <span data-ttu-id="10f2d-405">Le script **GazeCursor** est attaché à la **GazeCursor** objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-405">The script **GazeCursor** is attached to the **GazeCursor** object.</span></span>
- <span data-ttu-id="10f2d-406">Le script **SpatialMapping** est attaché à la **SpatialMapping** objet.</span><span class="sxs-lookup"><span data-stu-id="10f2d-406">The script **SpatialMapping** is attached to the **SpatialMapping** object.</span></span>
- <span data-ttu-id="10f2d-407">Dans [chapitre 5](#chapter-5---create-the-customvisionanalyser-class), étape 6 :</span><span class="sxs-lookup"><span data-stu-id="10f2d-407">In [Chapter 5](#chapter-5---create-the-customvisionanalyser-class), Step 6:</span></span>

    - <span data-ttu-id="10f2d-408">Assurez-vous que vous insérez votre **Service prédiction clé** dans le **predictionKey** variable.</span><span class="sxs-lookup"><span data-stu-id="10f2d-408">Make sure you insert your **Service Prediction Key** into the **predictionKey** variable.</span></span>
    - <span data-ttu-id="10f2d-409">Vous avez inséré votre **point de terminaison de prédiction** dans le **predictionEndpoint** classe.</span><span class="sxs-lookup"><span data-stu-id="10f2d-409">You have inserted your **Prediction Endpoint** into the **predictionEndpoint** class.</span></span>

## <a name="chapter-13---build-the-uwp-solution-and-sideload-your-application"></a><span data-ttu-id="10f2d-410">Chapitre 13 - générez la solution UWP et le chargement de version test, votre application</span><span class="sxs-lookup"><span data-stu-id="10f2d-410">Chapter 13 - Build the UWP solution and sideload your application</span></span>

<span data-ttu-id="10f2d-411">Vous êtes maintenant prêt à créer votre application en tant que UWP Solution auxquelles vous serez en mesure de déployer une session sur le Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="10f2d-411">You are now ready to build you application as a UWP Solution that you will be able to deploy on to the Microsoft HoloLens.</span></span> <span data-ttu-id="10f2d-412">Pour commencer le processus de génération :</span><span class="sxs-lookup"><span data-stu-id="10f2d-412">To begin the build process:</span></span>

1.  <span data-ttu-id="10f2d-413">Accédez à **fichier > Paramètres de Build**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-413">Go to **File > Build Settings**.</span></span>

2.  <span data-ttu-id="10f2d-414">Graduation **Unity C\# projets**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-414">Tick **Unity C\# Projects**.</span></span>

3.  <span data-ttu-id="10f2d-415">Cliquez sur **ajouter des scènes Open**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-415">Click on **Add Open Scenes**.</span></span> <span data-ttu-id="10f2d-416">Cette opération ajoute la scène actuellement ouverte à la build.</span><span class="sxs-lookup"><span data-stu-id="10f2d-416">This will add the currently open scene to the build.</span></span>

    ![](images/AzureLabs-Lab310-42.png)

4.  <span data-ttu-id="10f2d-417">Cliquez sur **Build**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-417">Click **Build**.</span></span> <span data-ttu-id="10f2d-418">Unity lancera un *Explorateur de fichiers* fenêtre, où vous avez besoin pour créer, puis sélectionnez un dossier pour générer l’application dans.</span><span class="sxs-lookup"><span data-stu-id="10f2d-418">Unity will launch a *File Explorer* window, where you need to create and then select a folder to build the app into.</span></span> <span data-ttu-id="10f2d-419">Créez ce dossier, puis nommez-le **application**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-419">Create that folder now, and name it **App**.</span></span> <span data-ttu-id="10f2d-420">Ensuite avec le **application** dossier sélectionné, cliquez sur **sélectionner le dossier**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-420">Then with the **App** folder selected, click **Select Folder**.</span></span>

5.  <span data-ttu-id="10f2d-421">Unity commencera à générer votre projet pour le **application** dossier.</span><span class="sxs-lookup"><span data-stu-id="10f2d-421">Unity will begin building your project to the **App** folder.</span></span>

6.  <span data-ttu-id="10f2d-422">Une fois Unity a fini de construction (il peut prendre un certain temps), celui-ci s’ouvre un **Explorateur de fichiers** fenêtre à l’emplacement de votre build (Vérifiez votre barre des tâches, tel qu’il ne peut pas toujours apparaître au-dessus de vos fenêtres, mais vous informera de l’ajout d’un nouveau fenêtre).</span><span class="sxs-lookup"><span data-stu-id="10f2d-422">Once Unity has finished building (it might take some time), it will open a **File Explorer** window at the location of your build (check your task bar, as it may not always appear above your windows, but will notify you of the addition of a new window).</span></span>

7.  <span data-ttu-id="10f2d-423">Pour déployer une session sur Microsoft HoloLens, vous devez l’adresse IP de cet appareil (pour les déployer à distance) et pour vous assurer qu’elle également a **Mode développeur** définie.</span><span class="sxs-lookup"><span data-stu-id="10f2d-423">To deploy on to Microsoft HoloLens, you will need the IP Address of that device (for Remote Deploy), and to ensure that it also has **Developer Mode** set.</span></span> <span data-ttu-id="10f2d-424">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="10f2d-424">To do this:</span></span>

    1.  <span data-ttu-id="10f2d-425">Tout en portant vos HoloLens, ouvrez le **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-425">Whilst wearing your HoloLens, open the **Settings**.</span></span>

    2.  <span data-ttu-id="10f2d-426">Accédez à **réseau & Internet** > **Wi-Fi** > **les Options avancées**</span><span class="sxs-lookup"><span data-stu-id="10f2d-426">Go to **Network & Internet** > **Wi-Fi** > **Advanced Options**</span></span>

    3.  <span data-ttu-id="10f2d-427">Remarque la **IPv4** adresse.</span><span class="sxs-lookup"><span data-stu-id="10f2d-427">Note the **IPv4** address.</span></span>

    4.  <span data-ttu-id="10f2d-428">Ensuite, accédez à **paramètres**, puis à **mise à jour & sécurité** > **pour les développeurs**</span><span class="sxs-lookup"><span data-stu-id="10f2d-428">Next, navigate back to **Settings**, and then to **Update & Security** > **For Developers**</span></span>

    5.  <span data-ttu-id="10f2d-429">Définissez **Mode développeur** *sur*.</span><span class="sxs-lookup"><span data-stu-id="10f2d-429">Set **Developer Mode** *On*.</span></span>

8.  <span data-ttu-id="10f2d-430">Accédez à votre nouvelle build Unity (le **application** dossier) et ouvrez le fichier solution avec **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-430">Navigate to your new Unity build (the **App** folder) and open the solution file with **Visual Studio**.</span></span>

9.  <span data-ttu-id="10f2d-431">Dans, sélectionnez la Configuration de Solution **déboguer**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-431">In the Solution Configuration select **Debug**.</span></span>

10. <span data-ttu-id="10f2d-432">Dans la plateforme de Solution, sélectionnez **x86, ordinateur distant**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-432">In the Solution Platform, select **x86, Remote Machine**.</span></span> <span data-ttu-id="10f2d-433">Vous devrez insérer le **adresse IP** d’un appareil distant (le Microsoft HoloLens, dans ce cas, que vous avez notée).</span><span class="sxs-lookup"><span data-stu-id="10f2d-433">You will be prompted to insert the **IP address** of a remote device (the Microsoft HoloLens, in this case, which you noted).</span></span>

    ![](images/AzureLabs-Lab310-43.png)

11. <span data-ttu-id="10f2d-434">Accédez à la **Build** menu et cliquez sur **déployer la Solution** à chargement indépendant de l’application à votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="10f2d-434">Go to the **Build** menu and click on **Deploy Solution** to sideload the application to your HoloLens.</span></span>

12. <span data-ttu-id="10f2d-435">Votre application doit maintenant apparaître dans la liste des applications installées sur votre Microsoft HoloLens, prêt à être lancé !</span><span class="sxs-lookup"><span data-stu-id="10f2d-435">Your app should now appear in the list of installed apps on your Microsoft HoloLens, ready to be launched!</span></span>

### <a name="to-use-the-application"></a><span data-ttu-id="10f2d-436">Pour utiliser l’application :</span><span class="sxs-lookup"><span data-stu-id="10f2d-436">To use the application:</span></span>

* <span data-ttu-id="10f2d-437">Examiner un objet, vous avez formé avec votre **Azure Custom Vision Service, la détection d’objets**et utiliser le **mouvement d’appui**.</span><span class="sxs-lookup"><span data-stu-id="10f2d-437">Look at an object, which you have trained with your **Azure Custom Vision Service, Object Detection**, and use the **Tap gesture**.</span></span>
* <span data-ttu-id="10f2d-438">Si l’objet est détecté, un espace universel *texte de l’étiquette* s’affiche avec le nom de balise.</span><span class="sxs-lookup"><span data-stu-id="10f2d-438">If the object is successfully detected, a world-space *Label Text* will appear with the tag name.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="10f2d-439">Chaque fois que vous capturez une photo et l’envoyez au Service, vous pouvez revenir à la page du Service et reformer le Service avec les images qui vient d’être capturées.</span><span class="sxs-lookup"><span data-stu-id="10f2d-439">Every time you capture a photo and send it to the Service, you can go back to the Service page and retrain the Service with the newly captured images.</span></span> <span data-ttu-id="10f2d-440">Au début, vous allez probablement également être amené à corriger le *englobants* pour être plus précis et de reformer le Service.</span><span class="sxs-lookup"><span data-stu-id="10f2d-440">At the beginning, you will probably also have to correct the *Bounding Boxes* to be more accurate and retrain the Service.</span></span>

> [!NOTE]
> <span data-ttu-id="10f2d-441">Le texte d’étiquette placée peuvent ne pas apparaître près de l’objet quand les capteurs Microsoft HoloLens et/ou le SpatialTrackingComponent dans Unity ne parvient pas à placer les colliders appropriés, par rapport aux objets du monde réel.</span><span class="sxs-lookup"><span data-stu-id="10f2d-441">The Label Text placed might not appear near the object when the Microsoft HoloLens sensors and/or the SpatialTrackingComponent in Unity fails to place the appropriate colliders, relative to the real world objects.</span></span> <span data-ttu-id="10f2d-442">Essayez d’utiliser l’application sur une surface différente si tel est le cas.</span><span class="sxs-lookup"><span data-stu-id="10f2d-442">Try to use the application on a different surface if that is the case.</span></span>

## <a name="your-custom-vision-object-detection-application"></a><span data-ttu-id="10f2d-443">Votre Vision personnalisée, application de détection d’objets</span><span class="sxs-lookup"><span data-stu-id="10f2d-443">Your Custom Vision, Object Detection application</span></span>

<span data-ttu-id="10f2d-444">Félicitations, vous avez créé une application de réalité mixte qui tire parti de la Vision personnalisée Azure, API de détection de l’objet, qui peut reconnaître un objet à partir d’une image, puis indiquent une position approximative pour cet objet dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="10f2d-444">Congratulations, you built a mixed reality app that leverages the Azure Custom Vision, Object Detection API, which can recognize an object from an image, and then provide an approximate position for that object in 3D space.</span></span>

![](images/AzureLabs-Lab310-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="10f2d-445">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="10f2d-445">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="10f2d-446">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="10f2d-446">Exercise 1</span></span>

<span data-ttu-id="10f2d-447">Ajout à l’étiquette de texte, utilisez un cube semi-transparent pour encapsuler l’objet réel dans une 3D *le rectangle englobant*.</span><span class="sxs-lookup"><span data-stu-id="10f2d-447">Adding to the Text Label, use a semi-transparent cube to wrap the real object in a 3D *Bounding Box*.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="10f2d-448">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="10f2d-448">Exercise 2</span></span>

<span data-ttu-id="10f2d-449">Formez votre Service de Vision personnalisée pour reconnaître des objets plus.</span><span class="sxs-lookup"><span data-stu-id="10f2d-449">Train your Custom Vision Service to recognize more objects.</span></span>

### <a name="exercise-3"></a><span data-ttu-id="10f2d-450">Exercice 3</span><span class="sxs-lookup"><span data-stu-id="10f2d-450">Exercise 3</span></span>

<span data-ttu-id="10f2d-451">Un signal sonore lorsqu’un objet est reconnu.</span><span class="sxs-lookup"><span data-stu-id="10f2d-451">Play a sound when an object is recognized.</span></span>

### <a name="exercise-4"></a><span data-ttu-id="10f2d-452">Exercice 4</span><span class="sxs-lookup"><span data-stu-id="10f2d-452">Exercise 4</span></span>

<span data-ttu-id="10f2d-453">Utiliser l’API pour recalculer votre Service avec les mêmes images de l’analyse de votre application, par conséquent, pour rendre le Service plus précis (effectuer la prédiction et la formation simultanément).</span><span class="sxs-lookup"><span data-stu-id="10f2d-453">Use the API to re-train your Service with the same images your app is analyzing, so to make the Service more accurate (do both prediction and training simultaneously).</span></span>
