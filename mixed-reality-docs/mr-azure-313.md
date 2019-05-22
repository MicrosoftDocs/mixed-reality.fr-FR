---
title: MR et Azure 313 - Service IoT Hub
description: Terminer ce cours pour apprendre à implémenter le Service Azure IoT Hub sur une machine virtuelle exécutant Ubuntu 16.4 et puis visualiser les données de message à l’aide de Microsoft HoloLens ou un casque (VR) immersif.
author: drneil
ms.author: jemccull
ms.date: 07/11/2018
ms.topic: article
keywords: réalité Azure, mixte, academy, edge, iot edge, didacticiel, api, notification, fonctions, tables, hololens, immersives, vr, iot, machine virtuelle, ubuntu, python
ms.openlocfilehash: 1ab7c48ac3cff1cb2283cadb171098af9e148628
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593254"
---
>[!NOTE]
><span data-ttu-id="b714d-104">Les didacticiels Académie de réalité mixte ont été conçus avec HoloLens (1er gen) et des casques IMMERSIFS réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="b714d-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="b714d-105">Par conséquent, nous estimons qu’il est important de laisser ces didacticiels en place pour les développeurs qui cherchent toujours pour obtenir des conseils de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="b714d-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="b714d-106">Ces didacticiels seront **_pas_** être mis à jour avec les ensembles d’outils ou les interactions utilisées pour HoloLens 2 dernières.</span><span class="sxs-lookup"><span data-stu-id="b714d-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="b714d-107">Ils seront conservées pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b714d-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="b714d-108">Il y aura une nouvelle série de didacticiels seront publiés dans le futur qui va vous montrer comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="b714d-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="b714d-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lorsqu’elles sont validées.</span><span class="sxs-lookup"><span data-stu-id="b714d-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-313-iot-hub-service"></a><span data-ttu-id="b714d-110">MR et Azure 313 : Service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b714d-110">MR and Azure 313: IoT Hub Service</span></span>

![résultat de cours](images/AzureLabs-Lab313-00.png)

<span data-ttu-id="b714d-112">Dans ce cours, vous allez apprendre à implémenter un **Service Azure IoT Hub** sur une machine virtuelle exécutant le système d’exploitation Ubuntu 16.4.</span><span class="sxs-lookup"><span data-stu-id="b714d-112">In this course, you will learn how to implement an **Azure IoT Hub Service** on a virtual machine running the Ubuntu 16.4 operating system.</span></span> <span data-ttu-id="b714d-113">Un **Azure Function App** servira pour recevoir des messages à partir de votre VM Ubuntu et stocker le résultat dans un **Service de Table Azure**.</span><span class="sxs-lookup"><span data-stu-id="b714d-113">An **Azure Function App** will then be used to receive messages from your Ubuntu VM, and store the result within an **Azure Table Service**.</span></span> <span data-ttu-id="b714d-114">Vous serez ensuite en mesure d’afficher ce à l’aide de données **Power BI** sur Microsoft HoloLens ou immersif casque (VR).</span><span class="sxs-lookup"><span data-stu-id="b714d-114">You will then be able to view this data using **Power BI** on Microsoft HoloLens or immersive (VR) headset.</span></span>

<span data-ttu-id="b714d-115">Le contenu de ce cours *est applicable* pour les appareils IoT Edge, bien que pour les besoins de ce cours, le focus sera dans un environnement de machine virtuelle, afin que l’accès à un périphérique de périmètre physique n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b714d-115">The content of this course *is applicable* to IoT Edge devices, though for the purpose of this course, the focus will be on a virtual machine environment, so that access to a physical Edge device is not necessary.</span></span>

<span data-ttu-id="b714d-116">En fin de ce didacticiel, vous allez apprendre à :</span><span class="sxs-lookup"><span data-stu-id="b714d-116">By completing this course, you will learn to:</span></span>

- <span data-ttu-id="b714d-117">Déployer un **module IoT Edge** à une Machine virtuelle (Ubuntu 16 OS), qui représentera votre appareil IoT.</span><span class="sxs-lookup"><span data-stu-id="b714d-117">Deploy an **IoT Edge module** to a Virtual Machine (Ubuntu 16 OS), which will represent your IoT device.</span></span>
- <span data-ttu-id="b714d-118">Ajouter un **Azure Custom Vision Tensorflow modèle** pour le module de Edge avec du code qui analysera les images stockées dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b714d-118">Add an **Azure Custom Vision Tensorflow Model** to the Edge module, with code that will analyze images stored in the container.</span></span>
- <span data-ttu-id="b714d-119">Configurer le module pour envoyer le message de résultat d’analyse à votre **Service IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b714d-119">Set up the module to send the analysis result message back to your **IoT Hub Service**.</span></span>
- <span data-ttu-id="b714d-120">Utilisez un **Azure Function App** pour stocker le message dans une **Table Azure**.</span><span class="sxs-lookup"><span data-stu-id="b714d-120">Use an **Azure Function App** to store the message within an **Azure Table**.</span></span>
- <span data-ttu-id="b714d-121">Configurer **Power BI** pour collecter les messages stocké et créer un rapport.</span><span class="sxs-lookup"><span data-stu-id="b714d-121">Set up **Power BI** to collect the stored message and create a report.</span></span>
- <span data-ttu-id="b714d-122">Visualisez vos données de message IoT dans **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="b714d-122">Visualize your IoT message data within **Power BI**.</span></span>

<span data-ttu-id="b714d-123">Les Services que vous allez utiliser sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="b714d-123">The Services you will use include:</span></span>

- <span data-ttu-id="b714d-124">**Azure IoT Hub** est un Service Microsoft Azure, ce qui permet aux développeurs de se connecter, surveiller et gérer des ressources IoT.</span><span class="sxs-lookup"><span data-stu-id="b714d-124">**Azure IoT Hub** is a Microsoft Azure Service which allows developers to connect, monitor, and manage, IoT assets.</span></span> <span data-ttu-id="b714d-125">Pour plus d’informations, visitez le [ **Service Azure IoT Hub** page](https://azure.microsoft.com/en-au/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="b714d-125">For more information, visit the [**Azure IoT Hub Service** page](https://azure.microsoft.com/en-au/services/iot-hub/).</span></span>

- <span data-ttu-id="b714d-126">**Azure Container Registry** est un Service Microsoft Azure, ce qui permet aux développeurs de stocker les images de conteneur pour différents types de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="b714d-126">**Azure Container Registry** is a Microsoft Azure Service which allows developers to store container images, for various types of containers.</span></span> <span data-ttu-id="b714d-127">Pour plus d’informations, visitez le [ **le Registre Azure Container Service** page](https://azure.microsoft.com/en-au/services/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="b714d-127">For more information, visit the [**Azure Container Registry Service** page](https://azure.microsoft.com/en-au/services/container-registry/).</span></span>

- <span data-ttu-id="b714d-128">**Azure Function App** est un Service Microsoft Azure, ce qui permet aux développeurs d’exécuter de petits morceaux de code, « fonctions », dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-128">**Azure Function App** is a Microsoft Azure Service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="b714d-129">Cela fournit un moyen permettant de déléguer le cloud, plutôt que votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="b714d-129">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="b714d-130">**Azure Functions** prend en charge plusieurs langages de développement, y compris C\#, F\#, Node.js, Java et PHP.</span><span class="sxs-lookup"><span data-stu-id="b714d-130">**Azure Functions** supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="b714d-131">Pour plus d’informations, visitez le [ **Azure Functions** page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="b714d-131">For more information, visit the [**Azure Functions** page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

- <span data-ttu-id="b714d-132">**Stockage Azure : Tables** est un Microsoft Azure Service, ce qui permet aux développeurs de stocker structurées, non SQL, les données dans le cloud, rendant facilement accessibles n’importe où.</span><span class="sxs-lookup"><span data-stu-id="b714d-132">**Azure Storage: Tables** is a Microsoft Azure Service, which allows developers to store structured, non-SQL, data in the cloud, making it easily accessible anywhere.</span></span> <span data-ttu-id="b714d-133">Le Service possède une conception sans schéma, permettant ainsi l’évolution des tables en fonction des besoins et il est donc très flexible.</span><span class="sxs-lookup"><span data-stu-id="b714d-133">The Service boasts a schema-less design, allowing for the evolution of tables as needed, and thus is very flexible.</span></span> <span data-ttu-id="b714d-134">Pour plus d’informations, visitez le [ **Tables Azure** page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span><span class="sxs-lookup"><span data-stu-id="b714d-134">For more information, visit the [**Azure Tables** page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span></span>

<span data-ttu-id="b714d-135">Ce cours va vous apprendre à configurer et utiliser le Service IoT Hub et ensuite visualiser une réponse fournie par un appareil.</span><span class="sxs-lookup"><span data-stu-id="b714d-135">This course will teach you how to setup and use the IoT Hub Service, and then visualize a response provided by a device.</span></span> <span data-ttu-id="b714d-136">Il le sera jusqu'à vous permettent d’appliquer ces concepts à une installation de Service IoT Hub personnalisée, vous voudrez peut-être générer.</span><span class="sxs-lookup"><span data-stu-id="b714d-136">It will be up to you to apply these concepts to a custom IoT Hub Service setup, which you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="b714d-137">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="b714d-137">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="b714d-138">Cours</span><span class="sxs-lookup"><span data-stu-id="b714d-138">Course</span></span></th><th style="width:150px"> <span data-ttu-id="b714d-139"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="b714d-139"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="b714d-140"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="b714d-140"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="b714d-141">MR et Azure 313 : Service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b714d-141">MR and Azure 313: IoT Hub Service</span></span></td><td style="text-align: center;"> <span data-ttu-id="b714d-142">✔️</span><span class="sxs-lookup"><span data-stu-id="b714d-142">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="b714d-143">✔️</span><span class="sxs-lookup"><span data-stu-id="b714d-143">✔️</span></span></td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="b714d-144">Prérequis</span><span class="sxs-lookup"><span data-stu-id="b714d-144">Prerequisites</span></span>

<span data-ttu-id="b714d-145">Pour les conditions préalables plus récentes pour le développement avec la réalité mixte, notamment avec le Microsoft HoloLens, visitez le [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article.</span><span class="sxs-lookup"><span data-stu-id="b714d-145">For the most up-to-date prerequisites for developing with mixed reality, including with the Microsoft HoloLens, visit the [Install the tools](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article.</span></span>

> [!NOTE]
> <span data-ttu-id="b714d-146">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base avec Python.</span><span class="sxs-lookup"><span data-stu-id="b714d-146">This tutorial is designed for developers who have basic experience with Python.</span></span> <span data-ttu-id="b714d-147">Veuillez également être conscient que les conditions préalables et les instructions écrites dans ce document représentent ce qui a été testé et vérifié au moment de l’écriture (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="b714d-147">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="b714d-148">Vous êtes libre d’utiliser la dernière version du logiciel, comme indiqué dans le [installer les outils](install-the-tools.md) article, même si elle pas supposer que les informations contenues dans ce cours seront parfaitement correspondre à ce que vous trouverez dans le logiciel plus récente que celle ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b714d-148">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than that listed below.</span></span>

<span data-ttu-id="b714d-149">Les matériels et logiciels suivants sont requises :</span><span class="sxs-lookup"><span data-stu-id="b714d-149">The following hardware and software is required:</span></span>

- <span data-ttu-id="b714d-150">Windows 10 Fall Creators Update (ou version ultérieure), **Mode développeur est activé**</span><span class="sxs-lookup"><span data-stu-id="b714d-150">Windows 10 Fall Creators Update (or later), **Developer Mode enabled**</span></span>

    > [!WARNING]
    > <span data-ttu-id="b714d-151">Vous ne pouvez pas exécuter une Machine virtuelle à l’aide de Hyper-V sur Windows 10 Édition familiale.</span><span class="sxs-lookup"><span data-stu-id="b714d-151">You cannot run a Virtual Machine using Hyper-V on Windows 10 Home Edition.</span></span>

- <span data-ttu-id="b714d-152">SDK Windows 10 (version la plus récente)</span><span class="sxs-lookup"><span data-stu-id="b714d-152">Windows 10 SDK (latest version)</span></span>
- <span data-ttu-id="b714d-153">Un HoloLens, **Mode développeur est activé**</span><span class="sxs-lookup"><span data-stu-id="b714d-153">A HoloLens, **Developer Mode enabled**</span></span>
- <span data-ttu-id="b714d-154">Visual Studio 2017.15.4 (utilisé uniquement pour accéder à l’Explorateur de Cloud Azure)</span><span class="sxs-lookup"><span data-stu-id="b714d-154">Visual Studio 2017.15.4 (Only used to access the Azure Cloud Explorer)</span></span>
- <span data-ttu-id="b714d-155">L’accès à Internet pour Azure et pour le Service IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b714d-155">Internet Access for Azure, and for IoT Hub Service.</span></span> <span data-ttu-id="b714d-156">Pour plus d’informations, veuillez suivre ce [lien vers la page du Service IoT Hub](https://azure.microsoft.com/en-au/services/iot-hub/)</span><span class="sxs-lookup"><span data-stu-id="b714d-156">For more information, please follow this [link to IoT Hub Service page](https://azure.microsoft.com/en-au/services/iot-hub/)</span></span>
- <span data-ttu-id="b714d-157">Un modèle d’apprentissage automatique.</span><span class="sxs-lookup"><span data-stu-id="b714d-157">A machine learning model.</span></span> <span data-ttu-id="b714d-158">Si vous n’avez pas votre propre prêtes à l’emploi de modèle, [vous pouvez utiliser le modèle fourni avec ce cours](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).</span><span class="sxs-lookup"><span data-stu-id="b714d-158">If you do not have your own ready to use model, [you can use the model provided with this course](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).</span></span>
- <span data-ttu-id="b714d-159">**Hyper-V** logiciel est activé sur votre ordinateur de développement Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b714d-159">**Hyper-V** software enabled on your Windows 10 development machine.</span></span>
- <span data-ttu-id="b714d-160">Une Machine virtuelle exécutant Ubuntu (16.4 ou 18.4), en cours d’exécution sur votre ordinateur de développement, ou vous pouvez également vous pouvez utiliser un ordinateur distinct exécutant Linux (Ubuntu 16.4 ou 18.4).</span><span class="sxs-lookup"><span data-stu-id="b714d-160">A Virtual Machine running Ubuntu (16.4 or 18.4), running on your development machine or alternatively you can use a separate computer running Linux (Ubuntu 16.4 or 18.4).</span></span> <span data-ttu-id="b714d-161">Vous trouverez plus d’informations sur la façon de créer une machine virtuelle sur Windows à l’aide de Hyper-V dans le [« Avant de commencer » de chapitre](#before-you-start). () https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="b714d-161">You can find more information on how to create a VM on Windows using Hyper-V in the ["Before you Start" chapter](#before-you-start).(https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).</span></span>  



### <a name="before-you-start"></a><span data-ttu-id="b714d-162">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b714d-162">Before you start</span></span>

1. <span data-ttu-id="b714d-163">Configurer et tester votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b714d-163">Set up and test your HoloLens.</span></span> <span data-ttu-id="b714d-164">Si vous avez besoin de prendre en charge de la configuration de votre HoloLens, [veillez à consulter l’article le programme d’installation de HoloLens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="b714d-164">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span>
2. <span data-ttu-id="b714d-165">Il est judicieux d’effectuer **étalonnage** et **capteur réglage** lorsque vous commencez le développement d’une nouvelle application HoloLens (parfois, il peut aider à effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="b714d-165">It is a good idea to perform **Calibration** and **Sensor Tuning** when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span>

<span data-ttu-id="b714d-166">Aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens).</span><span class="sxs-lookup"><span data-stu-id="b714d-166">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens).</span></span>

<span data-ttu-id="b714d-167">Pour une aide sur le réglage de capteur, veuillez suivre ce [lien vers l’article réglage de capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="b714d-167">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

3. <span data-ttu-id="b714d-168">Configurer votre **Machine virtuelle Ubuntu** à l’aide de **Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="b714d-168">Set up your **Ubuntu Virtual Machine** using **Hyper-V**.</span></span> <span data-ttu-id="b714d-169">Les ressources suivantes vous aideront avec le processus.</span><span class="sxs-lookup"><span data-stu-id="b714d-169">The following resources will help you with the process.</span></span>
    1.  <span data-ttu-id="b714d-170">Tout d’abord, suivez ce lien pour [télécharger le fichier ISO Ubuntu 16.04.4 LTS (Xenial Xerus)](http://au.releases.ubuntu.com/16.04/).</span><span class="sxs-lookup"><span data-stu-id="b714d-170">First, follow this link to [download the Ubuntu 16.04.4 LTS (Xenial Xerus) ISO](http://au.releases.ubuntu.com/16.04/).</span></span> <span data-ttu-id="b714d-171">Sélectionnez le **image de bureau de PC (AMD64) 64 bits**.</span><span class="sxs-lookup"><span data-stu-id="b714d-171">Select the **64-bit PC (AMD64) desktop image**.</span></span>
    2.  <span data-ttu-id="b714d-172">Assurez-vous que **Hyper-V** est activée sur votre ordinateur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b714d-172">Make sure **Hyper-V** is enabled on your Windows 10 machine.</span></span> <span data-ttu-id="b714d-173">Vous pouvez suivre ce lien pour obtenir des conseils sur [installation et l’activation d’Hyper-V sur Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="b714d-173">You can follow this link for guidance on [installing and enabling Hyper-V on Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span></span>
    3.  <span data-ttu-id="b714d-174">Démarrer Hyper-V et créer une nouvelle VM Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="b714d-174">Start Hyper-V and create a new Ubuntu VM.</span></span> <span data-ttu-id="b714d-175">Vous pouvez suivre ce lien pour une [guide étape par étape sur la façon de créer une machine virtuelle avec Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="b714d-175">You can follow this link for a [step by step guide on how to create a VM with Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine).</span></span> <span data-ttu-id="b714d-176">Lorsque la demande est **« Installer un système d’exploitation à partir d’un fichier image de démarrage »**, sélectionnez le **ISO Ubuntu** avoir téléchargement précédemment.</span><span class="sxs-lookup"><span data-stu-id="b714d-176">When requested to **"Install an operating system from a bootable image file"**, select the **Ubuntu ISO** you have download earlier.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b714d-177">À l’aide de **création rapide Hyper-V** n’est pas conseillée.</span><span class="sxs-lookup"><span data-stu-id="b714d-177">Using **Hyper-V Quick Create** is not suggested.</span></span>  

## <a name="chapter-1---retrieve-the-custom-vision-model"></a><span data-ttu-id="b714d-178">Chapitre 1 : récupérer le modèle de Vision personnalisée</span><span class="sxs-lookup"><span data-stu-id="b714d-178">Chapter 1 - Retrieve the Custom Vision model</span></span>

<span data-ttu-id="b714d-179">Grâce à ce cours, vous aurez accès à un [modèle de Vision personnalisée avant génération](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) qui détecte des claviers et des souris à partir d’images.</span><span class="sxs-lookup"><span data-stu-id="b714d-179">With this course you will have access to a [pre-built Custom Vision model](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) that detects keyboards and mice from images.</span></span> <span data-ttu-id="b714d-180">Si vous utilisez cette option, passez à [chapitre 2](#chapter-2---the-container-registry-service).</span><span class="sxs-lookup"><span data-stu-id="b714d-180">If you use this, proceed to [Chapter 2](#chapter-2---the-container-registry-service).</span></span>

<span data-ttu-id="b714d-181">Toutefois, vous pouvez suivre ces étapes si vous souhaitez utiliser votre propre modèle de Vision personnalisée :</span><span class="sxs-lookup"><span data-stu-id="b714d-181">However, you can follow these steps if you wish to use your own Custom Vision model:</span></span>

1. <span data-ttu-id="b714d-182">Dans votre **Custom Vision Project** accédez à la **performances** onglet.</span><span class="sxs-lookup"><span data-stu-id="b714d-182">In your **Custom Vision Project** go to the **Performance** tab.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b714d-183">Votre modèle doit utiliser un *compact* domaine, pour exporter le modèle.</span><span class="sxs-lookup"><span data-stu-id="b714d-183">Your model must use a *compact* domain, to export the model.</span></span> <span data-ttu-id="b714d-184">Vous pouvez modifier votre domaine de modèles dans les paramètres de votre projet.</span><span class="sxs-lookup"><span data-stu-id="b714d-184">You can change your models domain in the settings for your project.</span></span>

    ![onglet performances](images/AzureLabs-Lab313-01.png)

2. <span data-ttu-id="b714d-186">Sélectionnez le **itération** vous souhaitez exporter, puis cliquez sur **exporter**.</span><span class="sxs-lookup"><span data-stu-id="b714d-186">Select the **Iteration** you want to export and click on **Export**.</span></span> <span data-ttu-id="b714d-187">Un panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b714d-187">A blade will appear.</span></span>

    ![panneau d’exportation](images/AzureLabs-Lab313-02.png)

3. <span data-ttu-id="b714d-189">Dans le panneau, cliquez sur **fichier Docker**.</span><span class="sxs-lookup"><span data-stu-id="b714d-189">In the blade click **Docker File**.</span></span>

    ![Sélectionnez docker](images/AzureLabs-Lab313-03.png)

4. <span data-ttu-id="b714d-191">Cliquez sur **Linux** dans le menu déroulant et puis cliquez sur **télécharger**.</span><span class="sxs-lookup"><span data-stu-id="b714d-191">Click **Linux** in the drop-down menu and then click on **Download**.</span></span>

    ![Cliquez sur Télécharger](images/AzureLabs-Lab313-04.png)

5. <span data-ttu-id="b714d-193">Décompressez le contenu.</span><span class="sxs-lookup"><span data-stu-id="b714d-193">Unzip the content.</span></span> <span data-ttu-id="b714d-194">Vous l’utiliserez plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="b714d-194">You will use it later in this course.</span></span>

## <a name="chapter-2---the-container-registry-service"></a><span data-ttu-id="b714d-195">Chapitre 2 - le Service de Registre de conteneur</span><span class="sxs-lookup"><span data-stu-id="b714d-195">Chapter 2 - The Container Registry Service</span></span>

<span data-ttu-id="b714d-196">Le **Service de Registre de conteneur** est le référentiel utilisé pour héberger vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="b714d-196">The **Container Registry Service** is the repository used to host your containers.</span></span>

<span data-ttu-id="b714d-197">Le **Service IoT Hub** laquelle générer et utiliser dans ce cours, fait référence à **Service de Registre de conteneur** pour obtenir les conteneurs à déployer dans votre appareil Edge.</span><span class="sxs-lookup"><span data-stu-id="b714d-197">The **IoT Hub Service** that you will build and use in this course, refers to **Container Registry Service** to obtain the containers to deploy in your Edge Device.</span></span>

1. <span data-ttu-id="b714d-198">Tout d’abord, suivez ce [lien vers le portail Azure](https://portal.azure.com/)et connectez-vous avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="b714d-198">First, follow this [link to the Azure Portal](https://portal.azure.com/), and login with your credentials.</span></span>

2. <span data-ttu-id="b714d-199">Accédez à **créer une ressource** et recherchez **Registre de conteneurs**.</span><span class="sxs-lookup"><span data-stu-id="b714d-199">Go to **Create a resource** and look for **Container Registry**.</span></span>

    ![Registre de conteneurs](images/AzureLabs-Lab313-05.png)

3. <span data-ttu-id="b714d-201">Cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-201">Click on **Create**.</span></span>

    ![](images/AzureLabs-Lab313-06.png)

4. <span data-ttu-id="b714d-202">Configurer le Service de paramètres d’installation :</span><span class="sxs-lookup"><span data-stu-id="b714d-202">Set the Service setup parameters:</span></span>

    1. <span data-ttu-id="b714d-203">Insérez un nom pour votre projet, dans cet exemple ses appelée **IoTCRegistry**.</span><span class="sxs-lookup"><span data-stu-id="b714d-203">Insert a name for your project, In this example its called **IoTCRegistry**.</span></span>

    2. <span data-ttu-id="b714d-204">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b714d-204">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="b714d-205">Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-205">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="b714d-206">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="b714d-206">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

    3. <span data-ttu-id="b714d-207">Définissez l’emplacement du Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-207">Set the location of the Service.</span></span>

    4. <span data-ttu-id="b714d-208">Définissez **utilisateur_administrateur** à **activer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-208">Set **Admin user** to **Enable**.</span></span>

    5. <span data-ttu-id="b714d-209">Définissez **référence (SKU)** à **base**.</span><span class="sxs-lookup"><span data-stu-id="b714d-209">Set **SKU** to **Basic**.</span></span> 

    ![](images/AzureLabs-Lab313-07.png)

5. <span data-ttu-id="b714d-210">Cliquez sur **créer** et attendez que les Services doit être créé.</span><span class="sxs-lookup"><span data-stu-id="b714d-210">Click **Create** and wait for the Services to be created.</span></span> 

6. <span data-ttu-id="b714d-211">Une fois que la notification s’affiche vous informant de la création réussie de la *Registre de conteneurs*, cliquez sur **accéder à la ressource** d’être redirigé vers la page de votre Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-211">Once the notification pops up informing you of the successful creation of the *Container Registry*, click on **Go to resource** to be redirected to your Service page.</span></span>

    ![](images/AzureLabs-Lab313-08.png)

7. <span data-ttu-id="b714d-212">Dans le *Registre de conteneurs* page des services, cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="b714d-212">In the *Container Registry* Service page, click on **Access keys**.</span></span>

8. <span data-ttu-id="b714d-213">Prenez note (vous pouvez utiliser votre bloc-notes) des paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="b714d-213">Take note (you could use your Notepad) of the following parameters:</span></span>
    1. <span data-ttu-id="b714d-214">**Serveur de connexion**</span><span class="sxs-lookup"><span data-stu-id="b714d-214">**Login Server**</span></span>
    2. <span data-ttu-id="b714d-215">**Nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="b714d-215">**Username**</span></span>
    3. <span data-ttu-id="b714d-216">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="b714d-216">**Password**</span></span>

    ![](images/AzureLabs-Lab313-09.png)

## <a name="chapter-3---the-iot-hub-service"></a><span data-ttu-id="b714d-217">Chapitre 3 - le Service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="b714d-217">Chapter 3 - The IoT Hub Service</span></span>

<span data-ttu-id="b714d-218">Maintenant vous allez commencer la création et la configuration de votre **Service IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b714d-218">Now you will begin the creation and setup of your **IoT Hub Service**.</span></span>

1. <span data-ttu-id="b714d-219">Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b714d-219">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="b714d-220">Une fois connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **IoT Hub**, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="b714d-220">Once logged in, click on **Create a resource** in the top left corner, and search for **IoT Hub**, and click **Enter**.</span></span>

 ![Recherchez le compte de stockage](images/AzureLabs-Lab313-10.png)

3.  <span data-ttu-id="b714d-222">La nouvelle page doit fournir une description de la **compte de stockage** Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-222">The new page will provide a description of the **Storage account** Service.</span></span> <span data-ttu-id="b714d-223">En bas à gauche de cette invite, cliquez sur le **créer** bouton, pour créer une instance de ce Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-223">At the bottom left of this prompt, click the **Create** button, to create an instance of this Service.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-11.png)

4.  <span data-ttu-id="b714d-225">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b714d-225">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="b714d-226">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b714d-226">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="b714d-227">Un groupe de ressources offre un moyen pour surveiller, contrôler l’accès, approvisionner et gérer la facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-227">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="b714d-228">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="b714d-228">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="b714d-229">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="b714d-229">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>


    2. <span data-ttu-id="b714d-230">Sélectionnez un **emplacement** (utilisez le même emplacement pour tous les Services que vous créez dans ce cours).</span><span class="sxs-lookup"><span data-stu-id="b714d-230">Select an appropriate **Location** (Use the same location across all the Services you create in this course).</span></span>

    3. <span data-ttu-id="b714d-231">Insérez votre souhaitée **nom** pour cette instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-231">Insert your desired **Name** for this Service instance.</span></span>    

5.  <span data-ttu-id="b714d-232">En bas de la page, cliquez sur **suivant : Taille et échelle**.</span><span class="sxs-lookup"><span data-stu-id="b714d-232">On the bottom of the page click on **Next: Size and scale**.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-12.png)

6.  <span data-ttu-id="b714d-234">Dans cette page, sélectionnez votre **niveau de tarification et mise à l’échelle** (s’il s’agit de votre première instance de Service IoT Hub, une version gratuite doit être disponible pour vous).</span><span class="sxs-lookup"><span data-stu-id="b714d-234">In this page, select your **Pricing and scale tier** (if this is your first IoT Hub Service instance, a free tier should be available to you).</span></span>  

7.  <span data-ttu-id="b714d-235">Cliquez sur **vérifier + créer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-235">Click on **Review + Create**.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-13.png)

8.  <span data-ttu-id="b714d-237">Passez en revue vos paramètres, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-237">Review your settings and click on **Create**.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-14.png)

9. <span data-ttu-id="b714d-239">Une fois que la notification s’affiche vous informant de la création réussie de la *IoT Hub* Service, cliquez sur **accéder à la ressource** d’être redirigé vers la page de votre Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-239">Once the notification pops up informing you of the successful creation of the *IoT Hub* Service, click on **Go to resource** to be redirected to your Service page.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-15.png)

10. <span data-ttu-id="b714d-241">Faites défiler le panneau latéral gauche jusqu'à ce que vous voyiez *gestion automatique des appareils*, cliquez sur **IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-241">Scroll the side panel on the left until you see *Automatic Device Management*, the click on **IoT Edge**.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-16.png)

11. <span data-ttu-id="b714d-243">Dans la fenêtre qui apparaît à droite, cliquez sur **ajouter un appareil IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-243">In the window that appears to the right, click on **Add IoT Edge Device**.</span></span> <span data-ttu-id="b714d-244">Un panneau s’affiche à droite.</span><span class="sxs-lookup"><span data-stu-id="b714d-244">A blade will appear to the right.</span></span>

12. <span data-ttu-id="b714d-245">Dans le panneau, fournir votre nouvel appareil un **ID d’appareil** (il s’agit d’un nom de votre choix).</span><span class="sxs-lookup"><span data-stu-id="b714d-245">In the blade, provide your new device a **Device ID** (a name of your choice).</span></span> <span data-ttu-id="b714d-246">Ensuite, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-246">Then, click **Save**.</span></span> <span data-ttu-id="b714d-247">Le *principal* et *clés secondaires* auto génère, si vous avez **générer automatiquement** coché.</span><span class="sxs-lookup"><span data-stu-id="b714d-247">The *Primary* and *Secondary Keys* will auto generate, if you have **Auto Generate** ticked.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-17.png)

13. <span data-ttu-id="b714d-249">Vous permet d’accéder à la *appareils IoT Edge* section, dans laquelle votre nouvel appareil est répertoriée.</span><span class="sxs-lookup"><span data-stu-id="b714d-249">You will navigate back to the *IoT Edge Devices* section, where your new device will be listed.</span></span> <span data-ttu-id="b714d-250">Cliquez sur votre nouvel appareil (entourée en rouge dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="b714d-250">Click on your new device (outlined in red in the below image).</span></span> 

    ![créer l’instance de stockage](images/AzureLabs-Lab313-18.png)

14. <span data-ttu-id="b714d-252">Sur le *détails de l’appareil* page qui s’affiche, effectuez une copie de la **chaîne de connexion** (clé primaire).</span><span class="sxs-lookup"><span data-stu-id="b714d-252">On the *Device Details* page that appears, take a copy of the **Connection String** (primary key).</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-19.png)

15. <span data-ttu-id="b714d-254">Revenez au panneau sur la gauche, puis cliquez sur *stratégies d’accès partagé*, pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b714d-254">Go back to the panel on the left, and click *Shared access policies*, to open it.</span></span> 

16. <span data-ttu-id="b714d-255">Dans la page qui s’affiche, cliquez sur **iothubowner**, et un panneau s’affiche à droite de l’écran.</span><span class="sxs-lookup"><span data-stu-id="b714d-255">On the page that appears, click **iothubowner**, and a blade will appear to the right of the screen.</span></span> 

17. <span data-ttu-id="b714d-256">Prenez note (sur votre bloc-notes) de la **chaîne de connexion** (clé primaire), pour une utilisation ultérieure lors de la définition du *chaîne de connexion* à votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b714d-256">Take note (on your Notepad) of the **Connection string** (primary key), for later use when setting the *Connection String* to your device.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-20.png)

## <a name="chapter-4---setting-up-the-development-environment"></a><span data-ttu-id="b714d-258">Chapitre 4 - Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="b714d-258">Chapter 4 - Setting up the development environment</span></span>

<span data-ttu-id="b714d-259">Pour créer et déployer des modules pour *IoT Hub Edge*, vous aurez besoin des composants suivants sur votre ordinateur de développement exécutant Windows 10 :</span><span class="sxs-lookup"><span data-stu-id="b714d-259">In order to create and deploy modules for *IoT Hub Edge*, you will require the following components installed on your development machine running Windows 10:</span></span>

1.  <span data-ttu-id="b714d-260">[Docker pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), il vous sera demandé de créer un compte pour pouvoir télécharger.</span><span class="sxs-lookup"><span data-stu-id="b714d-260">[Docker for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), it will ask you to create an account to be able to download.</span></span> 

    <span data-ttu-id="b714d-261">[![téléchargement de docker pour windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)</span><span class="sxs-lookup"><span data-stu-id="b714d-261">[![download docker for windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b714d-262">Nécessite docker *Windows 10 PRO*, *Enterprise 14393*, ou *Windows Server 2016 RTM*, à exécuter.</span><span class="sxs-lookup"><span data-stu-id="b714d-262">Docker requires *Windows 10 PRO*, *Enterprise 14393*, or *Windows Server 2016 RTM*, to run.</span></span> <span data-ttu-id="b714d-263">Si d’autres versions de Windows 10 sont en cours d’exécution, vous pouvez essayer d’installer Docker en utilisant le [boîte à outils Docker](https://docs.docker.com/toolbox/toolbox_install_windows/).</span><span class="sxs-lookup"><span data-stu-id="b714d-263">If you are running other versions of Windows 10, you can try installing Docker using the [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/).</span></span>

2.  <span data-ttu-id="b714d-264">[Python 3.6](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="b714d-264">[Python 3.6](https://www.python.org/downloads/).</span></span>

    <span data-ttu-id="b714d-265">[![Téléchargez python 3.6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b714d-265">[![download python 3.6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)</span></span>

3.  <span data-ttu-id="b714d-266">[Visual Studio Code (également appelé VS Code)](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="b714d-266">[Visual Studio Code (also known as VS Code)](https://code.visualstudio.com/download).</span></span>

    <span data-ttu-id="b714d-267">[![Télécharger Visual Studio Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="b714d-267">[![download VS Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)</span></span>

<span data-ttu-id="b714d-268">Après avoir installé le logiciel mentionné ci-dessus, vous devrez redémarrer votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b714d-268">After installing the software mentioned above, you will need to restart your machine.</span></span>

## <a name="chapter-5---setting-up-the-ubuntu-environment"></a><span data-ttu-id="b714d-269">Chapitre 5 : configuration de l’environnement Ubuntu</span><span class="sxs-lookup"><span data-stu-id="b714d-269">Chapter 5 - Setting up the Ubuntu environment</span></span>

<span data-ttu-id="b714d-270">Maintenant vous pouvez passer à la configuration de votre appareil **en cours d’exécution du système d’exploitation Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="b714d-270">Now you can move on to setting up your device **running Ubuntu OS**.</span></span> <span data-ttu-id="b714d-271">Suivez les étapes ci-dessous pour installer le logiciel nécessaire, pour déployer vos conteneurs sur votre carte :</span><span class="sxs-lookup"><span data-stu-id="b714d-271">Follow the steps below, to install the necessary software, to deploy your containers on your board:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b714d-272">Vous devez toujours faire précéder les commandes terminal avec **sudo** à exécuter en tant qu’utilisateur administrateur.</span><span class="sxs-lookup"><span data-stu-id="b714d-272">You should always precede the terminal commands with **sudo** to run as admin user.</span></span> <span data-ttu-id="b714d-273">ex :</span><span class="sxs-lookup"><span data-stu-id="b714d-273">i.e:</span></span>
> 
>   ```bash
>   sudo docker \<option> \<command> \<argument>
>   ```

1.  <span data-ttu-id="b714d-274">Ouvrez le **Ubuntu Terminal**et utilisez la commande suivante pour installer **pip**:</span><span class="sxs-lookup"><span data-stu-id="b714d-274">Open the **Ubuntu Terminal**, and use the following command to install **pip**:</span></span>

    > [! Conseil]<span data-ttu-id="b714d-275"> vous pouvez ouvrir \*Terminal* très facilement à l’aide du raccourci clavier : *\*Ctrl + Alt + T*\*.</span><span class="sxs-lookup"><span data-stu-id="b714d-275"> You can open \*Terminal* very easily through using the keyboard shortcut: *\*Ctrl + Alt + T*\*.</span></span>

    ```bash
        sudo apt-get install python-pip
    ```

2.  <span data-ttu-id="b714d-276">Tout au long de ce chapitre, vous pouvez être invité, par *Terminal*d’autorisation d’utilisation du stockage de l’appareil et vous saisissiez **o/n** (Oui ou non), type **'y'**, puis appuyez sur la **Entrée** clé, à accepter.</span><span class="sxs-lookup"><span data-stu-id="b714d-276">Throughout this Chapter, you may be prompted, by *Terminal*, for permission to use your device storage, and for you to input **y/n** (yes or no), type **'y'**, and then press the **Enter** key, to accept.</span></span>

3.  <span data-ttu-id="b714d-277">Une fois cette commande terminée, utilisez la commande suivante pour installer **curl**:</span><span class="sxs-lookup"><span data-stu-id="b714d-277">Once that command has completed, use the following command to install **curl**:</span></span>

    ```bash
        sudo apt install curl
    ```

4.  <span data-ttu-id="b714d-278">Une fois **pip** et **curl** sont installés, utilisez la commande suivante pour installer le **runtime IoT Edge**, cela est nécessaire pour déployer et contrôler les modules sur votre carte :</span><span class="sxs-lookup"><span data-stu-id="b714d-278">Once **pip** and **curl** are installed, use the following command to install the **IoT Edge runtime**, this is necessary to deploy and control the modules on your board:</span></span>

    ```bash
        curl https://packages.microsoft.com/config/ubuntu/16.04/prod.list > ./microsoft-prod.list

        sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/

        curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg

        sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/

        sudo apt-get update

        sudo apt-get install moby-engine

        sudo apt-get install moby-cli

        sudo apt-get update

        sudo apt-get install iotedge
    ```

5. <span data-ttu-id="b714d-279">À ce stade vous êtes invité à ouvrir le *fichier de configuration de runtime*, pour insérer le **Device Connection String**, que vous avez notée (dans votre bloc-notes), lors de la création du **Service IoT Hub**  ([à l’étape 14, du chapitre 3](#chapter-3---the-iot-hub-service)).</span><span class="sxs-lookup"><span data-stu-id="b714d-279">At this point you will be prompted to open up the *runtime config file*, to insert the **Device Connection String**, that you noted down (in your Notepad), when creating the **IoT Hub Service** ([at step 14, of Chapter 3](#chapter-3---the-iot-hub-service)).</span></span> <span data-ttu-id="b714d-280">Exécutez la ligne suivante dans le terminal pour ouvrir ce fichier :</span><span class="sxs-lookup"><span data-stu-id="b714d-280">Run the following line on the terminal to open that file:</span></span>

    ```bash
        sudo nano /etc/iotedge/config.yaml
    ```

6. <span data-ttu-id="b714d-281">Le **config.yaml** fichier sera affichée, vous pouvez modifier :</span><span class="sxs-lookup"><span data-stu-id="b714d-281">The **config.yaml** file will be displayed, ready for you to edit:</span></span>

    > [!WARNING]
    > <span data-ttu-id="b714d-282">Lorsque ce fichier s’ouvre, il peut être prêter à confusion.</span><span class="sxs-lookup"><span data-stu-id="b714d-282">When this file opens, it may be somewhat confusing.</span></span> <span data-ttu-id="b714d-283">Vous serez dans ce fichier, l’édition de texte le *Terminal* lui-même.</span><span class="sxs-lookup"><span data-stu-id="b714d-283">You will be text editing this file, within the *Terminal* itself.</span></span> 

    1.  <span data-ttu-id="b714d-284">Utilisez les touches de direction de votre clavier pour faire défiler vers le bas (vous devez faire défiler de façon un peu) pour atteindre la ligne contenant « :</span><span class="sxs-lookup"><span data-stu-id="b714d-284">Use the arrow keys on your keyboard to scroll down (you will need to scroll down a little way), to reach the line containing":</span></span>

        <span data-ttu-id="b714d-285">"**\<AJOUTER ICI DEVICE CONNECTION STRING &GT;**".</span><span class="sxs-lookup"><span data-stu-id="b714d-285">"**\<ADD DEVICE CONNECTION STRING HERE>**".</span></span>

    2. <span data-ttu-id="b714d-286">Remplacez la ligne, **y compris les crochets**, avec le **Device Connection String** que vous avez noté précédemment.</span><span class="sxs-lookup"><span data-stu-id="b714d-286">Substitute line, **including the brackets**, with the **Device Connection String** you have noted earlier.</span></span>

7. <span data-ttu-id="b714d-287">Avec votre chaîne de connexion en place, sur votre clavier, appuyez sur la **Ctrl-X** clés pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="b714d-287">With your Connection String in place, on your keyboard, press the **Ctrl-X** keys to save the file.</span></span> <span data-ttu-id="b714d-288">Il vous demandera de confirmer en tapant **Y**. Ensuite, appuyez sur la **entrée** clé, pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="b714d-288">It will ask you to confirm by typing **Y**. Then, press the **Enter** key, to confirm.</span></span> <span data-ttu-id="b714d-289">Vous revenez à la mise à jour *Terminal*.</span><span class="sxs-lookup"><span data-stu-id="b714d-289">You will go back to the regular *Terminal*.</span></span> 

8. <span data-ttu-id="b714d-290">Une fois que ces commandes ont tous exécuté avec succès, vous avez installé le **Runtime de IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-290">Once these commands have all run successfully, you will have installed the **IoT Edge Runtime**.</span></span> <span data-ttu-id="b714d-291">Une fois initialisé, le runtime démarre sur son propre chaque fois que l’appareil est mis sous tension et sera placé dans l’arrière-plan, en attente pour les modules à déployer à partir de la **Service IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b714d-291">Once initialized, the runtime will start on its own every time the device is powered up, and will sit in the background, waiting for modules to be deployed from the **IoT Hub Service**.</span></span>

9.  <span data-ttu-id="b714d-292">Exécuter la ligne de commande suivante pour initialiser le *Runtime de IoT Edge*:</span><span class="sxs-lookup"><span data-stu-id="b714d-292">Run the following command line to initialize the *IoT Edge Runtime*:</span></span>

    ```bash
        sudo systemctl restart iotedge
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b714d-293">Si vous apportez des modifications à votre fichier .yaml ou la configuration ci-dessus, vous devez réexécuter la ligne de redémarrage ci-dessus, au sein de *Terminal*.</span><span class="sxs-lookup"><span data-stu-id="b714d-293">If you make changes to your .yaml file, or the above setup, you will need to run the above restart line again, within *Terminal*.</span></span>

10. <span data-ttu-id="b714d-294">Vérifier le *Runtime de IoT Edge* état en exécutant la ligne de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="b714d-294">Check the *IoT Edge Runtime* status by running the following command line.</span></span> <span data-ttu-id="b714d-295">Le runtime doit apparaître avec l’état **actif (en cours d’exécution)** en vert.</span><span class="sxs-lookup"><span data-stu-id="b714d-295">The runtime should appear with the status **active (running)** in green text.</span></span>

    ```bash
        sudo systemctl status iotedge
    ```

11. <span data-ttu-id="b714d-296">Appuyez sur la **Ctrl-C** clés, pour quitter la page d’état.</span><span class="sxs-lookup"><span data-stu-id="b714d-296">Press the **Ctrl-C** keys, to exit the status page.</span></span> <span data-ttu-id="b714d-297">Vous pouvez vérifier que le *Runtime de IoT Edge* extrait les conteneurs correctement en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-297">You can verify that the *IoT Edge Runtime* is pulling the containers correctly by typing the following command:</span></span>

    ```bash
        sudo docker ps
    ```

12. <span data-ttu-id="b714d-298">Une liste avec des conteneurs de deux (2) doit apparaître.</span><span class="sxs-lookup"><span data-stu-id="b714d-298">A list with two (2) containers should appear.</span></span> <span data-ttu-id="b714d-299">Il s’agit de modules par défaut qui sont automatiquement créés par le Service IoT Hub (edgeAgent et edgeHub).</span><span class="sxs-lookup"><span data-stu-id="b714d-299">These are the default modules that are automatically created by the IoT Hub Service (edgeAgent and edgeHub).</span></span> <span data-ttu-id="b714d-300">Une fois que vous créez et déployez vos propres modules, ils apparaîtront dans cette liste, en dessous de celles par défaut.</span><span class="sxs-lookup"><span data-stu-id="b714d-300">Once you create and deploy your own modules, they will appear in this list, underneath the default ones.</span></span>

## <a name="chapter-6---install-the-extensions"></a><span data-ttu-id="b714d-301">Chapitre 6 : installer les extensions</span><span class="sxs-lookup"><span data-stu-id="b714d-301">Chapter 6 - Install the extensions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b714d-302">Les chapitres suivants (6-9) ne doivent être exécutées sur votre ordinateur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="b714d-302">The next few Chapters (6-9) are to be performed on your Windows 10 machine.</span></span>

1. <span data-ttu-id="b714d-303">Ouvrez **VS Code**.</span><span class="sxs-lookup"><span data-stu-id="b714d-303">Open **VS Code**.</span></span>

2. <span data-ttu-id="b714d-304">Cliquez sur le **Extensions** bouton (carré) sur la gauche de VS Code barres, pour ouvrir le **panneau Extensions**.</span><span class="sxs-lookup"><span data-stu-id="b714d-304">Click on the **Extensions** (square) button on the left bar of VS Code, to open the **Extensions panel**.</span></span>

3. <span data-ttu-id="b714d-305">Rechercher et installer les extensions suivantes (comme indiqué dans l’image ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="b714d-305">Search for, and install, the following extensions (as shown in the image below):</span></span>

    1. <span data-ttu-id="b714d-306">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b714d-306">Azure IoT Edge</span></span>
    2. <span data-ttu-id="b714d-307">Kit de ressources Azure IoT</span><span class="sxs-lookup"><span data-stu-id="b714d-307">Azure IoT Toolkit</span></span>
    3. <span data-ttu-id="b714d-308">Docker</span><span class="sxs-lookup"><span data-stu-id="b714d-308">Docker</span></span>   

    ![Créez votre conteneur](images/AzureLabs-Lab313-24.png)

4. <span data-ttu-id="b714d-310">Une fois que les extensions sont installées, fermez et rouvrez VS Code.</span><span class="sxs-lookup"><span data-stu-id="b714d-310">Once the extensions are installed, close and re-open VS Code.</span></span>

5. <span data-ttu-id="b714d-311">Avec VS Code, ouvrez une fois de plus, accédez à **Affichage > terminal intégré**.</span><span class="sxs-lookup"><span data-stu-id="b714d-311">With VS Code open once more, navigate to **View > Integrated terminal**.</span></span>

6. <span data-ttu-id="b714d-312">Vous allez maintenant installer **Cookiecutter**.</span><span class="sxs-lookup"><span data-stu-id="b714d-312">You will now install **Cookiecutter**.</span></span> <span data-ttu-id="b714d-313">Dans le terminal, exécutez la commande bash suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-313">In the terminal run the following bash command:</span></span>

    ```bash
        pip install --upgrade --user cookiecutter
    ```

    > [! Conseil]<span data-ttu-id="b714d-314"> Si vous rencontrez des difficultés avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="b714d-314"> If you have trouble with this command:</span></span> 
    >1. <span data-ttu-id="b714d-315">Redémarrez VS Code, et / ou votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b714d-315">Restart VS Code, and/ or your computer.</span></span>
    >2. <span data-ttu-id="b714d-316">Il peut être nécessaire de basculer le **VS Code Terminal** à celle que vous avez utilisé pour installer Python, par exemple, **Powershell** (en particulier au cas où l’environnement Python a déjà été installée sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="b714d-316">It might be necessary to switch the **VS Code Terminal** to the one you have been using to install Python, i.e. **Powershell** (especially in case the Python environment was already installed on your machine).</span></span> <span data-ttu-id="b714d-317">Le Terminal ouvert, vous trouverez la liste déroulante sur le côté droit du Terminal.</span><span class="sxs-lookup"><span data-stu-id="b714d-317">With the Terminal open, you will find the drop down menu on the right side of the Terminal.</span></span>
     <span data-ttu-id="b714d-318">![Créez votre conteneur](images/AzureLabs-Lab313-24b.png)</span><span class="sxs-lookup"><span data-stu-id="b714d-318">![Create your container](images/AzureLabs-Lab313-24b.png)</span></span> 
    >3. <span data-ttu-id="b714d-319">Assurez-vous que le **Python** chemin d’installation est ajouté en tant que **Variable d’environnement** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b714d-319">Make sure the **Python** installation path is added as **Environment Variable** on your machine.</span></span> <span data-ttu-id="b714d-320">Cookiecutter doit faire partie de la même chemin d’accès d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="b714d-320">Cookiecutter should be part of the same location path.</span></span> <span data-ttu-id="b714d-321">Veuillez suivre ce [lien pour plus d’informations sur les Variables d’environnement](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx),</span><span class="sxs-lookup"><span data-stu-id="b714d-321">Please follow this [link for more information on Environment Variables](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx),</span></span> 

7. <span data-ttu-id="b714d-322">Une fois **Cookiecutter** a terminé l’installation, vous devez redémarrer votre ordinateur, afin que **Cookiecutter** est reconnu comme une commande, au sein de l’environnement de votre système.</span><span class="sxs-lookup"><span data-stu-id="b714d-322">Once **Cookiecutter** has finished installing, you should restart your machine, so that **Cookiecutter** is recognized as a command, within your System's environment.</span></span>

## <a name="chapter-7---create-your-container-solution"></a><span data-ttu-id="b714d-323">Chapitre 7 - créer votre solution de conteneurs</span><span class="sxs-lookup"><span data-stu-id="b714d-323">Chapter 7 - Create your container solution</span></span>

<span data-ttu-id="b714d-324">À ce stade, vous devez créer le conteneur, avec le module, pour être placé dans le *Registre de conteneurs*.</span><span class="sxs-lookup"><span data-stu-id="b714d-324">At this point, you need to create the container, with the module, to be pushed into the *Container Registry*.</span></span> <span data-ttu-id="b714d-325">Une fois que vous avez envoyé votre conteneur, vous allez utiliser le *IoT Hub Edge* Service à la déployer sur votre appareil, ce qui est en cours d’exécution le *runtime IoT Edge*.</span><span class="sxs-lookup"><span data-stu-id="b714d-325">Once you have pushed your container, you will use the *IoT Hub Edge* Service to deploy it to your device, which is running the *IoT Edge runtime*.</span></span>

1. <span data-ttu-id="b714d-326">À partir du Code de Visual Studio, cliquez sur **vue > palette de commandes**.</span><span class="sxs-lookup"><span data-stu-id="b714d-326">From VS Code, click **View > Command palette**.</span></span>

2. <span data-ttu-id="b714d-327">Dans la palette, rechercher et exécuter **Azure IoT Edge : Nouvelle Solution Iot Edge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-327">In the palette, search and run **Azure IoT Edge: New Iot Edge Solution**.</span></span>

3. <span data-ttu-id="b714d-328">Naviguer dans un emplacement où vous souhaitez créer votre solution.</span><span class="sxs-lookup"><span data-stu-id="b714d-328">Browse into a location where you want to create your solution.</span></span> <span data-ttu-id="b714d-329">Appuyez sur la **entrée** clé, pour accepter l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="b714d-329">Press the **Enter** key, to accept the location.</span></span>

4. <span data-ttu-id="b714d-330">Donnez un nom à votre solution.</span><span class="sxs-lookup"><span data-stu-id="b714d-330">Give a name to your solution.</span></span> <span data-ttu-id="b714d-331">Appuyez sur la **entrée** clé, pour confirmer votre nom fourni.</span><span class="sxs-lookup"><span data-stu-id="b714d-331">Press the **Enter** key, to confirm your provided name.</span></span>

5. <span data-ttu-id="b714d-332">Vous devez maintenant choisir le framework de modèle pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="b714d-332">Now you will be prompted to choose the template framework for your solution.</span></span> <span data-ttu-id="b714d-333">Cliquez sur **Module Python**.</span><span class="sxs-lookup"><span data-stu-id="b714d-333">Click **Python Module**.</span></span> <span data-ttu-id="b714d-334">Appuyez sur la **entrée** clé, pour confirmer ce choix.</span><span class="sxs-lookup"><span data-stu-id="b714d-334">Press the **Enter** key, to confirm this choice.</span></span>

6. <span data-ttu-id="b714d-335">Donnez un nom à votre module.</span><span class="sxs-lookup"><span data-stu-id="b714d-335">Give a name to your module.</span></span> <span data-ttu-id="b714d-336">Appuyez sur la **entrée** clé, pour confirmer le nom de votre module.</span><span class="sxs-lookup"><span data-stu-id="b714d-336">Press the **Enter** key, to confirm the name of your module.</span></span> <span data-ttu-id="b714d-337">Veillez à prendre note (avec votre bloc-notes) du nom du module, comme nous l’utiliserons ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b714d-337">Make sure to take a note (with your Notepad) of the module name, as it is used later.</span></span>

7. <span data-ttu-id="b714d-338">Vous pouvez remarquer un prédéfinis *référentiel d’images Docker* adresse apparaîtra dans la palette.</span><span class="sxs-lookup"><span data-stu-id="b714d-338">You will notice a pre-built *Docker Image Repository* address will appear on the palette.</span></span> <span data-ttu-id="b714d-339">Il doit ressembler :</span><span class="sxs-lookup"><span data-stu-id="b714d-339">It will look like:</span></span>

    <span data-ttu-id="b714d-340">**localhost:5000 /-nom de votre MODULE -**.</span><span class="sxs-lookup"><span data-stu-id="b714d-340">**localhost:5000/-THE NAME OF YOUR MODULE-**.</span></span> 

8. <span data-ttu-id="b714d-341">Supprimer **localhost:5000**et dans son insertion place le *Container Registry* **serveur de connexion** adresse que vous avez notée lors de la création du **conteneur Service de Registre** ([à l’étape 8, chapitre 2](#chapter-2---the-container-registry-service)).</span><span class="sxs-lookup"><span data-stu-id="b714d-341">Delete **localhost:5000**, and in its place insert the *Container Registry* **Login Server** address, which you noted when creating the **Container Registry Service** ([in step 8, of Chapter 2](#chapter-2---the-container-registry-service)).</span></span> <span data-ttu-id="b714d-342">Appuyez sur la **entrée** clé, pour confirmer l’adresse.</span><span class="sxs-lookup"><span data-stu-id="b714d-342">Press the **Enter** key, to confirm the address.</span></span>

9. <span data-ttu-id="b714d-343">À ce stade, la solution qui contient le modèle pour votre module Python sera créée et sa structure s’affichera dans le **onglet Explorer**, de Visual Studio Code, sur le côté gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="b714d-343">At this point, the solution containing the template for your Python module will be created and its structure will be displayed in the **Explore Tab**, of VS Code, on the left side of the screen.</span></span> <span data-ttu-id="b714d-344">Si le **onglet Explorer** est pas ouverte, vous pouvez l’ouvrir en cliquant sur le bouton le plus haut, dans la barre de gauche.</span><span class="sxs-lookup"><span data-stu-id="b714d-344">If the **Explore Tab** is not open, you can open it by clicking the top-most button, in the bar on the left.</span></span>

    ![Créez votre conteneur](images/AzureLabs-Lab313-25.png)

10. <span data-ttu-id="b714d-346">La dernière étape de ce chapitre, est de cliquer sur et ouvrez le **fichier .env**, depuis le **onglet Explorer**et ajoutez votre *Registre de conteneurs* **nom d’utilisateur** et **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b714d-346">The last step for this Chapter, is to click and open the **.env file**, from within the **Explore Tab**, and add your *Container Registry* **username** and **password**.</span></span> <span data-ttu-id="b714d-347">Ce fichier est ignoré par git, mais sur la création du conteneur, définit les informations d’identification pour accéder à la **Service de Registre de conteneur**.</span><span class="sxs-lookup"><span data-stu-id="b714d-347">This file is ignored by git, but on building the container, will set the credentials to access the **Container Registry Service**.</span></span>

    ![Créez votre conteneur](images/AzureLabs-Lab313-26.png)

## <a name="chapter-8---editing-your-container-solution"></a><span data-ttu-id="b714d-349">Chapitre 8 - modification de votre solution de conteneurs</span><span class="sxs-lookup"><span data-stu-id="b714d-349">Chapter 8 - Editing your container solution</span></span>

<span data-ttu-id="b714d-350">Vous allez maintenant effectuer la solution de conteneur, en mettant à jour les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="b714d-350">You will now complete the container solution, by updating the following files:</span></span>

- <span data-ttu-id="b714d-351">*principal<span></span>.py* script python.</span><span class="sxs-lookup"><span data-stu-id="b714d-351">*main<span></span>.py* python script.</span></span>
- <span data-ttu-id="b714d-352">*requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="b714d-352">*requirements.txt*.</span></span>
- <span data-ttu-id="b714d-353">*deployment.template.json*.</span><span class="sxs-lookup"><span data-stu-id="b714d-353">*deployment.template.json*.</span></span>
- <span data-ttu-id="b714d-354">*Dockerfile.amd64*</span><span class="sxs-lookup"><span data-stu-id="b714d-354">*Dockerfile.amd64*</span></span>

<span data-ttu-id="b714d-355">Vous allez ensuite créer le *images* dossier, utilisé par le script python pour rechercher les images à mettre en correspondance votre *modèle de Vision personnalisée*.</span><span class="sxs-lookup"><span data-stu-id="b714d-355">You will then create the *images* folder, used by the python script to check for images to match against your *Custom Vision model*.</span></span> <span data-ttu-id="b714d-356">Enfin, vous allez ajouter le *labels.txt* fichier, pour aider à lire votre modèle et le *model.pb* fichier, qui est votre modèle.</span><span class="sxs-lookup"><span data-stu-id="b714d-356">Lastly, you will add the *labels.txt* file, to help read your model, and the *model.pb* file, which is your model.</span></span>

1. <span data-ttu-id="b714d-357">Avec VS Code ouvrir, accédez à votre dossier de module et recherchez le script appelé **principal<span></span>.py**.</span><span class="sxs-lookup"><span data-stu-id="b714d-357">With VS Code open, navigate to your module folder, and look for the script called **main<span></span>.py**.</span></span> <span data-ttu-id="b714d-358">Double-cliquez pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b714d-358">Double-click to open it.</span></span>

2. <span data-ttu-id="b714d-359">Supprimer le contenu du fichier et insérez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b714d-359">Delete the content of the file and insert the following code:</span></span>

    ```python
    # Copyright (c) Microsoft. All rights reserved.
    # Licensed under the MIT license. See LICENSE file in the project root for
    # full license information.

    import random
    import sched, time
    import sys
    import iothub_client
    from iothub_client import IoTHubModuleClient, IoTHubClientError, IoTHubTransportProvider
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError
    import json
    import os
    import tensorflow as tf
    import os
    from PIL import Image
    import numpy as np
    import cv2

    # messageTimeout - the maximum time in milliseconds until a message times out.
    # The timeout period starts at IoTHubModuleClient.send_event_async.
    # By default, messages do not expire.
    MESSAGE_TIMEOUT = 10000

    # global counters
    RECEIVE_CALLBACKS = 0
    SEND_CALLBACKS = 0

    TEMPERATURE_THRESHOLD = 25
    TWIN_CALLBACKS = 0

    # Choose HTTP, AMQP or MQTT as transport protocol.  Currently only MQTT is supported.
    PROTOCOL = IoTHubTransportProvider.MQTT


    # Callback received when the message that we're forwarding is processed.
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )


    def convert_to_opencv(image):
        # RGB -> BGR conversion is performed as well.
        r,g,b = np.array(image).T
        opencv_image = np.array([b,g,r]).transpose()
        return opencv_image

    def crop_center(img,cropx,cropy):
        h, w = img.shape[:2]
        startx = w//2-(cropx//2)
        starty = h//2-(cropy//2)
        return img[starty:starty+cropy, startx:startx+cropx]

    def resize_down_to_1600_max_dim(image):
        h, w = image.shape[:2]
        if (h < 1600 and w < 1600):
            return image

        new_size = (1600 * w // h, 1600) if (h > w) else (1600, 1600 * h // w)
        return cv2.resize(image, new_size, interpolation = cv2.INTER_LINEAR)

    def resize_to_256_square(image):
        h, w = image.shape[:2]
        return cv2.resize(image, (256, 256), interpolation = cv2.INTER_LINEAR)

    def update_orientation(image):
        exif_orientation_tag = 0x0112
        if hasattr(image, '_getexif'):
            exif = image._getexif()
            if (exif != None and exif_orientation_tag in exif):
                orientation = exif.get(exif_orientation_tag, 1)
                # orientation is 1 based, shift to zero based and flip/transpose based on 0-based values
                orientation -= 1
                if orientation >= 4:
                    image = image.transpose(Image.TRANSPOSE)
                if orientation == 2 or orientation == 3 or orientation == 6 or orientation == 7:
                    image = image.transpose(Image.FLIP_TOP_BOTTOM)
                if orientation == 1 or orientation == 2 or orientation == 5 or orientation == 6:
                    image = image.transpose(Image.FLIP_LEFT_RIGHT)
        return image


    def analyse(hubManager):

        messages_sent = 0;

        while True:
            #def send_message():
            print ("Load the model into the project")
            # These names are part of the model and cannot be changed.
            output_layer = 'loss:0'
            input_node = 'Placeholder:0'

            graph_def = tf.GraphDef()
            labels = []

            labels_filename = "labels.txt"
            filename = "model.pb"

            # Import the TF graph
            with tf.gfile.FastGFile(filename, 'rb') as f:
                graph_def.ParseFromString(f.read())
                tf.import_graph_def(graph_def, name='')

            # Create a list of labels
            with open(labels_filename, 'rt') as lf:
                for l in lf:
                    labels.append(l.strip())
            print ("Model loaded into the project")

            results_dic = dict()

            # create the JSON to be sent as a message
            json_message = ''

            # Iterate through images 
            print ("List of images to analyse:")
            for file in os.listdir('images'):
                print(file)

                image = Image.open("images/" + file)

                # Update orientation based on EXIF tags, if the file has orientation info.
                image = update_orientation(image)

                # Convert to OpenCV format
                image = convert_to_opencv(image)

                # If the image has either w or h greater than 1600 we resize it down respecting
                # aspect ratio such that the largest dimension is 1600
                image = resize_down_to_1600_max_dim(image)

                # We next get the largest center square
                h, w = image.shape[:2]
                min_dim = min(w,h)
                max_square_image = crop_center(image, min_dim, min_dim)

                # Resize that square down to 256x256
                augmented_image = resize_to_256_square(max_square_image)

                # The compact models have a network size of 227x227, the model requires this size.
                network_input_size = 227

                # Crop the center for the specified network_input_Size
                augmented_image = crop_center(augmented_image, network_input_size, network_input_size)

                try:
                    with tf.Session() as sess:     
                        prob_tensor = sess.graph.get_tensor_by_name(output_layer)
                        predictions, = sess.run(prob_tensor, {input_node: [augmented_image] })
                except Exception as identifier:
                    print ("Identifier error: ", identifier)

                print ("Print the highest probability label")
                highest_probability_index = np.argmax(predictions)
                print('FINAL RESULT! Classified as: ' + labels[highest_probability_index])

                l = labels[highest_probability_index]

                results_dic[file] = l

                # Or you can print out all of the results mapping labels to probabilities.
                label_index = 0
                for p in predictions:
                    truncated_probablity = np.float64(round(p,8))
                    print (labels[label_index], truncated_probablity)
                    label_index += 1

            print("Results dictionary")
            print(results_dic)

            json_message = json.dumps(results_dic)
            print("Json result")
            print(json_message)

            # Initialize a new message
            message = IoTHubMessage(bytearray(json_message, 'utf8'))
        
            hubManager.send_event_to_output("output1", message, 0)

            messages_sent += 1
            print("Message sent! - Total: " + str(messages_sent))      
            print('----------------------------')
            
            # This is the wait time before repeating the analysis
            # Currently set to 10 seconds
            time.sleep(10)


    class HubManager(object):
        
        def __init__(
                self,
                protocol=IoTHubTransportProvider.MQTT):
            self.client_protocol = protocol
            self.client = IoTHubModuleClient()
            self.client.create_from_environment(protocol)

            # set the time until a message times out
            self.client.set_option("messageTimeout", MESSAGE_TIMEOUT)

        # Forwards the message received onto the next stage in the process.
        def forward_event_to_output(self, outputQueueName, event, send_context):
            self.client.send_event_async(
                outputQueueName, event, send_confirmation_callback, send_context)

        def send_event_to_output(self, outputQueueName, event, send_context):
            self.client.send_event_async(outputQueueName, event, send_confirmation_callback, send_context)

    def main(protocol):
        try:
            hub_manager = HubManager(protocol)
            analyse(hub_manager)
            while True:
                time.sleep(1)

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubModuleClient sample stopped" )

    if __name__ == '__main__':
        main(PROTOCOL)
    ```

3.  <span data-ttu-id="b714d-360">Ouvrez le fichier appelé **requirements.txt**, puis remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b714d-360">Open the file called **requirements.txt**, and substitute its content with the following:</span></span>

    ```
    azure-iothub-device-client==1.4.0.0b3
    opencv-python==3.3.1.11
    tensorflow==1.8.0
    pillow==5.1.0
    ```

4.  <span data-ttu-id="b714d-361">Ouvrez le fichier appelé **deployment.template.json**, puis remplacez son contenu suivant le ci-dessous indication :</span><span class="sxs-lookup"><span data-stu-id="b714d-361">Open the file called **deployment.template.json**, and substitute its content following the below guideline:</span></span>

    1. <span data-ttu-id="b714d-362">Étant donné que vous avez votre propre, unique, structure JSON, vous devrez modifier manuellement (au lieu de copier un exemple).</span><span class="sxs-lookup"><span data-stu-id="b714d-362">Because you will have your own, unique, JSON structure, you will need to edit it by hand (rather than copying an example).</span></span> <span data-ttu-id="b714d-363">Pour faciliter la tâche, utilisez l’image en tant que guide ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b714d-363">To make this easy, use the below image as a guide.</span></span>
    2. <span data-ttu-id="b714d-364">Les zones qui aura un aspect différents à la vôtre, mais que vous **ne devez pas modifier sont mis en surbrillance jaune**.</span><span class="sxs-lookup"><span data-stu-id="b714d-364">Areas which will look different to yours, but which you **should NOT change are highlighted yellow**.</span></span>
    3. <span data-ttu-id="b714d-365">**Les sections dont vous avez besoin à supprimer, sont mis en surbrillance rouge.**</span><span class="sxs-lookup"><span data-stu-id="b714d-365">**Sections which you need to delete, are a highlighted red.**</span></span>
    4. <span data-ttu-id="b714d-366">Veillez à supprimer les crochets corrects et également supprimer les virgules.</span><span class="sxs-lookup"><span data-stu-id="b714d-366">Be careful to delete the correct brackets, and also remove the commas.</span></span>

        ![Créez votre conteneur](images/AzureLabs-Lab313-27.png)

    5. <span data-ttu-id="b714d-368">Le JSON terminé doit ressembler à l’image suivante (Cependant, avec votre différences uniques : *références de nom d’utilisateur/mot de passe/nom/un module*) :</span><span class="sxs-lookup"><span data-stu-id="b714d-368">The completed JSON should look like the following image (though, with your unique differences: *username/password/module name/module references*):</span></span>

        ![Créez votre conteneur](images/AzureLabs-Lab313-28.png)

5.  <span data-ttu-id="b714d-370">Ouvrez le fichier appelé **Dockerfile.amd64**, puis remplacez son contenu par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="b714d-370">Open the file called **Dockerfile.amd64**, and substitute its content with the following:</span></span>

    ```
    FROM ubuntu:xenial

    WORKDIR /app

    RUN apt-get update && \
        apt-get install -y --no-install-recommends libcurl4-openssl-dev python-pip libboost-python-dev && \
        rm -rf /var/lib/apt/lists/* 
    RUN pip install --upgrade pip
    RUN pip install setuptools

    COPY requirements.txt ./
    RUN pip install -r requirements.txt

    RUN pip install pillow
    RUN pip install numpy

    RUN apt-get update && apt-get install -y \ 
        pkg-config \
        python-dev \ 
        python-opencv \ 
        libopencv-dev \ 
        libav-tools  \ 
        libjpeg-dev \ 
        libpng-dev \ 
        libtiff-dev \ 
        libjasper-dev \ 
        python-numpy \ 
        python-pycurl \ 
        python-opencv


    RUN pip install opencv-python
    RUN pip install tensorflow
    RUN pip install --upgrade tensorflow

    COPY . .

    RUN useradd -ms /bin/bash moduleuser
    USER moduleuser

    CMD [ "python", "-u", "./main.py" ]

    ```

6.  <span data-ttu-id="b714d-371">Avec le bouton droit sur le dossier sous **modules** (il aura le nom que vous avez fourni précédemment ; dans l’exemple vers le bas, il est appelé *pythonmodule*), puis cliquez sur **nouveau dossier**.</span><span class="sxs-lookup"><span data-stu-id="b714d-371">Right-click on the folder beneath **modules** (it will have the name you provided previously; in the example further down, it is called *pythonmodule*), and click on **New Folder**.</span></span> <span data-ttu-id="b714d-372">Nommez le dossier **images**.</span><span class="sxs-lookup"><span data-stu-id="b714d-372">Name the folder **images**.</span></span>

7.  <span data-ttu-id="b714d-373">Dans le dossier, ajouter des images contenant la souris ou le clavier.</span><span class="sxs-lookup"><span data-stu-id="b714d-373">Inside the folder, add some images containing mouse or keyboard.</span></span> <span data-ttu-id="b714d-374">Ceux-ci seront les images qui seront analysées par le modèle Tensorflow.</span><span class="sxs-lookup"><span data-stu-id="b714d-374">Those will be the images that will be analyzed by the Tensorflow model.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b714d-375">Si vous utilisez votre propre modèle, vous devez modifier pour refléter vos propres données de modèles.</span><span class="sxs-lookup"><span data-stu-id="b714d-375">If you are using your own model, you will need to change this to reflect your own models data.</span></span>

8.  <span data-ttu-id="b714d-376">Vous devez maintenant récupérer le **labels.txt** et **model.pb** à partir du dossier de modèle que vous avez téléchargé les fichiers (ou créé à partir de votre propre **Service Vision personnalisée** ), dans [chapitre 1](#chapter-1---retrieve-the-custom-vision-model).</span><span class="sxs-lookup"><span data-stu-id="b714d-376">You will now need to retrieve the **labels.txt** and **model.pb** files from the model folder, which you previous downloaded (or created from your own **Custom Vision Service**), in [Chapter 1](#chapter-1---retrieve-the-custom-vision-model).</span></span> <span data-ttu-id="b714d-377">Une fois que vous disposez des fichiers, les placer dans votre solution, en même temps que les autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="b714d-377">Once you have the files, place them within your solution, alongside the other files.</span></span> <span data-ttu-id="b714d-378">Le résultat final doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b714d-378">The final result should look like the image below:</span></span>

    ![Créez votre conteneur](images/AzureLabs-Lab313-29.png)

## <a name="chapter-9---package-the-solution-as-a-container"></a><span data-ttu-id="b714d-380">Chapitre 9 - Package de la solution en tant que conteneur</span><span class="sxs-lookup"><span data-stu-id="b714d-380">Chapter 9 - Package the solution as a container</span></span>

1.  <span data-ttu-id="b714d-381">Vous êtes maintenant prêt à « package » de vos fichiers en tant que conteneur et les distribuer à vos **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="b714d-381">You are now ready to "package" your files as a container and push it to your **Azure Container Registry**.</span></span> <span data-ttu-id="b714d-382">Dans VS Code, ouvrez le *Terminal intégré* (**Affichage > Terminal intégré / CTRL + '**) et utilisez la ligne suivante pour vous connecter à **Docker** (remplacez les valeurs de la commande avec les informations d’identification de votre **Azure Container Registry (ACR)**) :</span><span class="sxs-lookup"><span data-stu-id="b714d-382">Within VS Code, open the *Integrated Terminal* (**View > Integrated Terminal / CTRL + \`**), and use the following line to login to **Docker** (substitute the values of the command with the credentials of your **Azure Container Registry (ACR)**):</span></span>

    ```bash
        docker login -u <ACR username> -p <ACR password> <ACR login server>
    ```

2. <span data-ttu-id="b714d-383">Avec le bouton droit sur le fichier **deployment.template.json**, puis cliquez sur **générer la Solution IoT Edge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-383">Right-click on the file **deployment.template.json**, and click **Build IoT Edge Solution**.</span></span> <span data-ttu-id="b714d-384">Ce processus de génération prend un certain temps (en fonction de votre appareil), préparez-vous à attendre.</span><span class="sxs-lookup"><span data-stu-id="b714d-384">This build process takes quite some time (depending on your device), so be prepared to wait.</span></span> <span data-ttu-id="b714d-385">Une fois le processus de génération est terminée, un **Deployment.JSON ainsi** fichier sera créé à l’intérieur d’un nouveau dossier appelé **config**.</span><span class="sxs-lookup"><span data-stu-id="b714d-385">After the build process finishes, a **deployment.json** file will have been created inside a new folder called **config**.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-30.png)

3. <span data-ttu-id="b714d-387">Ouvrez le **Palette de commandes** à nouveau et recherchez **Azure : Connectez-vous**.</span><span class="sxs-lookup"><span data-stu-id="b714d-387">Open the **Command Palette** again, and search for **Azure: Sign In**.</span></span> <span data-ttu-id="b714d-388">Suivez les invites à l’aide de vos informations d’identification du compte Azure ; VS Code vous fournira une option permettant de *copier et ouvrir*, qui copiera le code de l’appareil vous aurez bientôt besoin et ouvrez votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="b714d-388">Follow the prompts using your Azure Account credentials; VS Code will provide you with an option to *Copy and Open*, which will copy the device code you will soon need, and open your default web browser.</span></span> <span data-ttu-id="b714d-389">Lorsque vous êtes invité, collez le code de l’appareil, pour authentifier votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b714d-389">When asked, paste the device code, to authenticate your machine.</span></span>

    ![copier et ouvrir](images/AzureLabs-Lab313-31.png)

4. <span data-ttu-id="b714d-391">Une fois signé en vous remarquerez, sur le côté inférieur de la *Explorer* panneau, une nouvelle section appelée **appareils Azure IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b714d-391">Once signed in you will notice, on the bottom side of the *Explore* panel, a new section called **Azure IoT Hub Devices**.</span></span> <span data-ttu-id="b714d-392">Cliquez sur cette section pour la développer.</span><span class="sxs-lookup"><span data-stu-id="b714d-392">Click this section to expand it.</span></span>

    ![APPAREIL Edge](images/AzureLabs-Lab313-32.png)

5. <span data-ttu-id="b714d-394">Si votre appareil n’est pas ici, vous devrez avec le bouton droit *appareils Azure IoT Hub*, puis cliquez sur **définir la chaîne de connexion IoT Hub**.</span><span class="sxs-lookup"><span data-stu-id="b714d-394">If your device is not here, you will need to right-click *Azure IoT Hub Devices*, and then click **Set IoT Hub Connection String**.</span></span> <span data-ttu-id="b714d-395">Vous verrez ensuite que le **Palette de commandes** (en haut de VS Code), vous invitera à entrer votre *chaîne de connexion*.</span><span class="sxs-lookup"><span data-stu-id="b714d-395">You will then see that the **Command Palette** (at the top of VS Code), will prompt you to input your *Connection String*.</span></span> <span data-ttu-id="b714d-396">Il s’agit du *chaîne de connexion* que vous avez noté à la fin de [chapitre 3](#chapter-3---the-iot-hub-service).</span><span class="sxs-lookup"><span data-stu-id="b714d-396">This is the *Connection String* you noted down at the end of [Chapter 3](#chapter-3---the-iot-hub-service).</span></span> <span data-ttu-id="b714d-397">Appuyez sur la **entrée** de clé, une fois que vous avez copiée dans la chaîne de.</span><span class="sxs-lookup"><span data-stu-id="b714d-397">Press the **Enter** key, once you have copied the string in.</span></span>    

6. <span data-ttu-id="b714d-398">Votre appareil doit charger et s’affichent.</span><span class="sxs-lookup"><span data-stu-id="b714d-398">Your device should load, and appear.</span></span> <span data-ttu-id="b714d-399">Avec le bouton droit sur le nom du périphérique, puis cliquez sur, **créer un déploiement pour un seul appareil**.</span><span class="sxs-lookup"><span data-stu-id="b714d-399">Right-click on the device name, and then click, **Create Deployment for Single Device**.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-33b.png)

7. <span data-ttu-id="b714d-401">Vous obtiendrez un *Explorateur de fichiers* invite, où vous pouvez accéder à la **config** dossier, puis sélectionnez le **Deployment.JSON ainsi** fichier.</span><span class="sxs-lookup"><span data-stu-id="b714d-401">You will get a *File Explorer* prompt, where you can navigate to the **config** folder, and then select the **deployment.json** file.</span></span> <span data-ttu-id="b714d-402">Ce fichier est sélectionné, cliquez sur le **sélectionner un manifeste de déploiement Edge** bouton.</span><span class="sxs-lookup"><span data-stu-id="b714d-402">With that file selected, click the **Select Edge Deployment Manifest** button.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-34.png)

8. <span data-ttu-id="b714d-404">À ce stade, vous avez fourni votre **Service IoT Hub** avec le manifeste pour pouvoir déployer votre conteneur, en tant que module, à partir de votre **Azure Container Registry**, efficacement déployer sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="b714d-404">At this point you have provided your **IoT Hub Service** with the manifest for it to deploy your container, as a module, from your **Azure Container Registry**, effectively deploying it to your device.</span></span>

9. <span data-ttu-id="b714d-405">Pour afficher les messages envoyés à partir de votre appareil à IoT Hub, avec le bouton droit à nouveau sur le nom de votre appareil dans le **appareils Azure IoT Hub** section, dans le **Explorer** panneau, puis cliquez sur **démarrer l’analyse D2C Message**.</span><span class="sxs-lookup"><span data-stu-id="b714d-405">To view the messages sent from your device to the IoT Hub, right-click again on your device name in the **Azure IoT Hub Devices** section, in the **Explorer** panel, and click on **Start Monitoring D2C Message**.</span></span> <span data-ttu-id="b714d-406">Les messages envoyés à partir de votre appareil doivent apparaître dans le Terminal VS.</span><span class="sxs-lookup"><span data-stu-id="b714d-406">The messages sent from your device should appear in the VS Terminal.</span></span> <span data-ttu-id="b714d-407">Soyez patient, comme cela peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="b714d-407">Be patient, as this may take some time.</span></span> <span data-ttu-id="b714d-408">Consultez le chapitre suivant pour le débogage et en vérifiant si le déploiement a réussi.</span><span class="sxs-lookup"><span data-stu-id="b714d-408">See the next Chapter for debugging, and checking if deployment was successful.</span></span>

<span data-ttu-id="b714d-409">Ce module effectuera une itération maintenant entre les images dans le **images** dossier et les analyser, avec chaque itération.</span><span class="sxs-lookup"><span data-stu-id="b714d-409">This module will now iterate between the images in the **images** folder and analyze them, with each iteration.</span></span> <span data-ttu-id="b714d-410">Il s’agit évidemment juste une démonstration illustrant comment obtenir le modèle de base de machine learning pour travailler dans un environnement d’appareil IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="b714d-410">This is obviously just a demonstration of how to get the basic machine learning model to work in an IoT Edge device environment.</span></span> 

<span data-ttu-id="b714d-411">Pour développer les fonctionnalités de cet exemple, peut procéder de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="b714d-411">To expand the functionality of this example, you could proceed in several ways.</span></span> <span data-ttu-id="b714d-412">Une façon pourrait être, y compris du code dans le conteneur, qui capture des photos à partir d’une webcam qui est connecté à l’appareil et enregistre les images dans le dossier images.</span><span class="sxs-lookup"><span data-stu-id="b714d-412">One way could be including some code in the container, that captures photos from a webcam that is connected to the device, and saves the images in the images folder.</span></span> 

<span data-ttu-id="b714d-413">Une autre façon pouvez copier les images à partir de l’appareil IoT dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="b714d-413">Another way could be copying the images from the IoT device into the container.</span></span> <span data-ttu-id="b714d-414">Un moyen pratique de le faire consiste à exécuter la commande suivante dans l’appareil IoT Terminal Server (peut-être une petite application Impossible d’effectuer la tâche, si vous voulez automatiser le processus).</span><span class="sxs-lookup"><span data-stu-id="b714d-414">A practical way to do that is to run the following command in the IoT device Terminal (perhaps a small app could do the job, if you wished to automate the process).</span></span> <span data-ttu-id="b714d-415">Vous pouvez tester cette commande en exécutant manuellement à partir de l’emplacement du dossier où sont stockés vos fichiers :</span><span class="sxs-lookup"><span data-stu-id="b714d-415">You can test this command by running it manually from the folder location where your files are stored:</span></span>

```bash
    sudo docker cp <filename> <modulename>:/app/images/<a name of your choice>
```

## <a name="chapter-10---debugging-the-iot-edge-runtime"></a><span data-ttu-id="b714d-416">Chapitre 10 - débogage du Runtime IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b714d-416">Chapter 10 - Debugging the IoT Edge Runtime</span></span>

<span data-ttu-id="b714d-417">Voici une liste des lignes de commande et obtenir des conseils, pour vous aider à surveiller et déboguer l’activité de messagerie de le *Runtime de IoT Edge*, à partir de votre **appareil Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="b714d-417">The following are a list of command lines, and tips, to help you monitor and debug the messaging activity of the *IoT Edge Runtime*, from your **Ubuntu device**.</span></span> 

- <span data-ttu-id="b714d-418">Vérifier le *Runtime de IoT Edge* état en exécutant la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-418">Check the *IoT Edge Runtime* status by running the following command line:</span></span>

    ```bash
        sudo systemctl status iotedge
    ```

    > [!NOTE]
    > <span data-ttu-id="b714d-419">N’oubliez pas d’appuyer sur **Ctrl + C**, pour terminer l’affichage de l’état.</span><span class="sxs-lookup"><span data-stu-id="b714d-419">Remember to press **Ctrl + C**, to finish viewing the status.</span></span>

- <span data-ttu-id="b714d-420">Répertorier les conteneurs qui sont actuellement déployées.</span><span class="sxs-lookup"><span data-stu-id="b714d-420">List the containers that are currently deployed.</span></span> <span data-ttu-id="b714d-421">Si le *Service IoT Hub* a déployé les conteneurs, ils seront affichés en exécutant la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-421">If the *IoT Hub Service* has deployed the containers successfully, they will be displayed by running the following command line:</span></span>

    ```bash
        sudo iotedge list
    ```

    <span data-ttu-id="b714d-422">Ou</span><span class="sxs-lookup"><span data-stu-id="b714d-422">Or</span></span>

    ```bash
        sudo docker ps
    ```

    > [!NOTE]
    > <span data-ttu-id="b714d-423">La méthode ci-dessus est un bon moyen pour vérifier si votre module a été correctement déployé, tel qu’il apparaîtra dans la liste ; vous allez sinon **uniquement** voir le *edgeHub* et *edgeAgent*.</span><span class="sxs-lookup"><span data-stu-id="b714d-423">The above is a good way to check whether your module has been deployed successfully, as it will appear in the list; you will otherwise **only** see the *edgeHub* and *edgeAgent*.</span></span>

- <span data-ttu-id="b714d-424">Pour afficher les journaux de code d’un conteneur, exécutez la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-424">To display the code logs of a container, run the following command line:</span></span>

    ```bash
        journalctl -u iotedge
    ```

<span data-ttu-id="b714d-425">**Commandes utiles pour gérer le Runtime IoT Edge :**</span><span class="sxs-lookup"><span data-stu-id="b714d-425">**Useful commands to manage the IoT Edge Runtime:**</span></span>

-  <span data-ttu-id="b714d-426">Pour supprimer tous les conteneurs dans l’hôte :</span><span class="sxs-lookup"><span data-stu-id="b714d-426">To delete all containers in the host:</span></span>

    ```bash
        sudo docker rm -f $(sudo docker ps -aq)
    ```

-  <span data-ttu-id="b714d-427">Pour arrêter la *Runtime de IoT Edge*:</span><span class="sxs-lookup"><span data-stu-id="b714d-427">To stop the *IoT Edge Runtime*:</span></span>

    ```bash
        sudo systemctl stop iotedge
    ```

## <a name="chapter-11---create-table-service"></a><span data-ttu-id="b714d-428">Chapitre 11 - créer le Service de Table</span><span class="sxs-lookup"><span data-stu-id="b714d-428">Chapter 11 - Create Table Service</span></span> 

<span data-ttu-id="b714d-429">Accédez à votre portail Azure, où vous allez créer un Service de Tables Azure, en créant une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="b714d-429">Navigate back to your Azure Portal, where you will create an Azure Tables Service, by creating a Storage resource.</span></span>

1. <span data-ttu-id="b714d-430">Si pas déjà connecté, connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b714d-430">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="b714d-431">Une fois connecté, cliquez sur **créer une ressource**, dans le coin supérieur gauche de coin et recherchez **compte de stockage**, puis appuyez sur la **entrée** clé, la recherche doit commencer.</span><span class="sxs-lookup"><span data-stu-id="b714d-431">Once logged in, click on **Create a resource**, in the top left corner, and search for **Storage account**, and press the **Enter** key, to start the search.</span></span>

3. <span data-ttu-id="b714d-432">Une fois que l’application s’affiche, cliquez sur **compte de stockage - blob, fichier, table, file d’attente** à partir de la liste.</span><span class="sxs-lookup"><span data-stu-id="b714d-432">Once it has appeared, click **Storage account - blob, file, table, queue** from the list.</span></span>

    ![Recherchez le compte de stockage](images/AzureLabs-Lab313-35.png)

4. <span data-ttu-id="b714d-434">La nouvelle page doit fournir une description de la **compte de stockage** Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-434">The new page will provide a description of the **Storage account** Service.</span></span> <span data-ttu-id="b714d-435">En bas à gauche de cette invite, cliquez sur le **créer** bouton, pour créer une instance de ce Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-435">At the bottom left of this prompt, click the **Create** button, to create an instance of this Service.</span></span>

    ![créer l’instance de stockage](images/AzureLabs-Lab313-36.png)

5. <span data-ttu-id="b714d-437">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="b714d-437">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="b714d-438">Insérez votre souhaitée **nom** pour cette instance de Service (*doit être en minuscules*).</span><span class="sxs-lookup"><span data-stu-id="b714d-438">Insert your desired **Name** for this Service instance (*must be all lowercase*).</span></span>

    2. <span data-ttu-id="b714d-439">Pour **modèle de déploiement**, cliquez sur **Resource manager**.</span><span class="sxs-lookup"><span data-stu-id="b714d-439">For **Deployment model**, click **Resource manager**.</span></span>

    3. <span data-ttu-id="b714d-440">Pour **type de compte**, utilisez le menu déroulant, cliquez sur **stockage (usage général v1)**.</span><span class="sxs-lookup"><span data-stu-id="b714d-440">For **Account kind**, using the dropdown menu, click **Storage (general purpose v1)**.</span></span>

    4. <span data-ttu-id="b714d-441">Cliquez sur un texte approprié **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="b714d-441">Click an appropriate **Location**.</span></span>
    
    5. <span data-ttu-id="b714d-442">Pour le **réplication** menu déroulant, cliquez sur **en lecture-access-geo-redundant storage (RA-GRS)**.</span><span class="sxs-lookup"><span data-stu-id="b714d-442">For the **Replication** dropdown menu, click **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6. <span data-ttu-id="b714d-443">Pour **performances**, cliquez sur **Standard**.</span><span class="sxs-lookup"><span data-stu-id="b714d-443">For **Performance**, click **Standard**.</span></span>

    7. <span data-ttu-id="b714d-444">Dans le **transfert sécurisé requis** , cliquez sur **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="b714d-444">Within the **Secure transfer required** section, click **Disabled**.</span></span>

    8. <span data-ttu-id="b714d-445">À partir de la **abonnement** menu déroulant, cliquez sur un abonnement approprié.</span><span class="sxs-lookup"><span data-stu-id="b714d-445">From the **Subscription** dropdown menu, click an appropriate subscription.</span></span>

    9. <span data-ttu-id="b714d-446">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b714d-446">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="b714d-447">Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-447">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="b714d-448">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="b714d-448">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="b714d-449">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="b714d-449">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="b714d-450">Laissez **réseaux virtuels** comme **désactivé**, s’il s’agit d’une option pour vous.</span><span class="sxs-lookup"><span data-stu-id="b714d-450">Leave **Virtual networks** as **Disabled**, if this is an option for you.</span></span>

    11. <span data-ttu-id="b714d-451">Cliquez sur **Create (Créer)**.</span><span class="sxs-lookup"><span data-stu-id="b714d-451">Click **Create**.</span></span>

        ![Renseignez les détails de stockage](images/AzureLabs-Lab313-37.png)

6. <span data-ttu-id="b714d-453">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="b714d-453">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

7. <span data-ttu-id="b714d-454">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="b714d-454">A notification will appear in the Portal once the Service instance is created.</span></span> <span data-ttu-id="b714d-455">Cliquez sur les notifications pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-455">Click on the notifications to explore your new Service instance.</span></span>

    ![nouvelle notification de stockage](images/AzureLabs-Lab313-38.png)

8. <span data-ttu-id="b714d-457">Cliquez sur le **accéder à la ressource** bouton dans la notification et vous serez dirigé vers votre nouvelle page de vue d’ensemble d’instance Service de stockage.</span><span class="sxs-lookup"><span data-stu-id="b714d-457">Click the **Go to resource** button in the notification, and you will be taken to your new Storage Service instance overview page.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab313-39.png)

9. <span data-ttu-id="b714d-459">Dans la page Vue d’ensemble, à droite, cliquez sur **Tables**.</span><span class="sxs-lookup"><span data-stu-id="b714d-459">From the overview page, to the right-hand side, click **Tables**.</span></span>
    
    ![Tables](images/AzureLabs-Lab313-40.png)

10. <span data-ttu-id="b714d-461">Le volet de droite change et indique le **Service de Table** plus d’informations, dans laquelle vous devez ajouter une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="b714d-461">The panel on the right will change to show the **Table Service** information, wherein you need to add a new table.</span></span> <span data-ttu-id="b714d-462">Cela en cliquant sur le **+ Table** bouton vers le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="b714d-462">Do this by clicking the **+ Table** button to the top-left corner.</span></span>

    ![ouvrir des Tables](images/AzureLabs-Lab313-41.png)

11. <span data-ttu-id="b714d-464">Une nouvelle page s’affiche, dans laquelle vous devez entrer un **nom de la Table**.</span><span class="sxs-lookup"><span data-stu-id="b714d-464">A new page will be shown, wherein you need to enter a **Table name**.</span></span> <span data-ttu-id="b714d-465">Il s’agit du nom que vous utiliserez pour faire référence aux données dans votre application dans les chapitres (création d’application de fonction et Power BI).</span><span class="sxs-lookup"><span data-stu-id="b714d-465">This is the name you will use to refer to the data in your application in later Chapters (creating Function App, and Power BI).</span></span> <span data-ttu-id="b714d-466">Insérer **IoTMessages** comme nom (vous pouvez choisir votre propre, n’oubliez pas qu’il lorsqu’il est utilisé plus loin dans ce document) et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b714d-466">Insert **IoTMessages** as the name (you can choose your own, just remember it when used later in this document) and click **OK**.</span></span> 

12. <span data-ttu-id="b714d-467">Une fois que la nouvelle table a été créée, vous serez en mesure de voir dans le **Service de Table** page (en bas).</span><span class="sxs-lookup"><span data-stu-id="b714d-467">Once the new table has been created, you will be able to see it within the **Table Service** page (at the bottom).</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-42.png)  

13. <span data-ttu-id="b714d-469">Cliquez maintenant sur **clés d’accès** et effectuez une copie de la **nom de compte de stockage** et **clé** (à l’aide de votre bloc-notes), vous utiliserez ces valeurs plus loin dans ce cours, lorsque vous créez le **Azure Function App**.</span><span class="sxs-lookup"><span data-stu-id="b714d-469">Now click on **Access keys** and take a copy of the **Storage account name** and **Key** (using your Notepad), you will use these values later in this course, when creating the **Azure Function App**.</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-43.png) 

14. <span data-ttu-id="b714d-471">Utilisation du Panneau de gauche à nouveau, faites défiler vers le *Service de Table* section, puis cliquez sur **Tables** (ou **parcourir les Tables**, dans les portails plus récente) et effectuez une copie de la  **URL de la table** (à l’aide de votre bloc-notes).</span><span class="sxs-lookup"><span data-stu-id="b714d-471">Using the panel on the left again, scroll to the *Table Service* section, and click **Tables** (or **Browse Tables**, in newer Portals) and take a copy of the **Table URL** (using your Notepad).</span></span> <span data-ttu-id="b714d-472">Vous utiliserez cette valeur plus loin dans ce cours, lors de la liaison de votre table à votre **Power BI** application.</span><span class="sxs-lookup"><span data-stu-id="b714d-472">You will use this value later in this course, when linking your table to your **Power BI** application.</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-44.png)

## <a name="chapter-12---completing-the-azure-table"></a><span data-ttu-id="b714d-474">Chapitre 12 - fin de la Table Azure</span><span class="sxs-lookup"><span data-stu-id="b714d-474">Chapter 12 - Completing the Azure Table</span></span>

<span data-ttu-id="b714d-475">Maintenant que votre **Service de Table** compte de stockage a été configuré, il est temps d’ajouter des données, qui sera utilisé pour stocker et récupérer des informations.</span><span class="sxs-lookup"><span data-stu-id="b714d-475">Now that your **Table Service** storage account has been setup, it is time to add data to it, which will be used to store and retrieve information.</span></span> <span data-ttu-id="b714d-476">La modification de vos Tables peut être effectuée via **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="b714d-476">The editing of your Tables can be done through **Visual Studio**.</span></span>

1. <span data-ttu-id="b714d-477">Ouvrez **Visual Studio** (**pas** Visual Studio Code).</span><span class="sxs-lookup"><span data-stu-id="b714d-477">Open **Visual Studio** (**not** Visual Studio Code).</span></span>

2. <span data-ttu-id="b714d-478">Dans le menu, cliquez sur **Affichage > Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-478">From the menu, click **View > Cloud Explorer**.</span></span>

    ![Ouvrez cloud explorer](images/AzureLabs-Lab313-45.png)

3. <span data-ttu-id="b714d-480">Le **Cloud Explorer** s’ouvre comme un élément ancré (patient, comme le chargement peut prendre un temps).</span><span class="sxs-lookup"><span data-stu-id="b714d-480">The **Cloud Explorer** will open as a docked item (be patient, as loading may take time).</span></span>

    > [!WARNING] 
    > <span data-ttu-id="b714d-481">Si l’abonnement que vous avez utilisé pour créer votre *comptes de stockage* n’est pas visible, assurez-vous d’avoir :</span><span class="sxs-lookup"><span data-stu-id="b714d-481">If the subscription you used to create your *Storage Accounts* is not visible, ensure that you have:</span></span> 
    > - <span data-ttu-id="b714d-482">Ouvert une session le même compte que celui utilisé pour le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-482">Logged in to the same account as the one you used for the Azure Portal.</span></span>
    > - <span data-ttu-id="b714d-483">Sélectionné de votre abonnement à partir de la page de gestion des comptes (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :</span><span class="sxs-lookup"><span data-stu-id="b714d-483">Selected your subscription from the Account Management page (you may need to apply a filter from your account settings):</span></span>  
    >
    >   ![trouver un abonnement](images/AzureLabs-Lab313-46.png)

4. <span data-ttu-id="b714d-485">Vos Services cloud Azure seront affichera.</span><span class="sxs-lookup"><span data-stu-id="b714d-485">Your Azure cloud Services will be shown.</span></span> <span data-ttu-id="b714d-486">Rechercher **comptes de stockage** et cliquez sur la flèche à gauche de cette option pour développer vos comptes.</span><span class="sxs-lookup"><span data-stu-id="b714d-486">Find **Storage Accounts** and click the arrow to the left of that to expand your accounts.</span></span>

    ![ouvrir des comptes de stockage](images/AzureLabs-Lab313-47.png)

5. <span data-ttu-id="b714d-488">Une fois développé, vous avez récemment créé **compte de stockage** doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="b714d-488">Once expanded, your newly created **Storage account** should be available.</span></span> <span data-ttu-id="b714d-489">Cliquez sur la flèche à gauche de votre stockage et recherchez une fois qui est développé, **Tables** et cliquez sur la flèche à côté de cela, pour faire apparaître le **Table** vous avez créé dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="b714d-489">Click the arrow to the left of your storage, and then once that is expanded, find **Tables** and click the arrow next to that, to reveal the **Table** you created in the last Chapter.</span></span> <span data-ttu-id="b714d-490">Double-cliquez sur votre **Table**.</span><span class="sxs-lookup"><span data-stu-id="b714d-490">Double-click your **Table**.</span></span>

6. <span data-ttu-id="b714d-491">Votre table sera ouvert dans le centre de la fenêtre Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b714d-491">Your table will be opened in the center of your Visual Studio window.</span></span> <span data-ttu-id="b714d-492">Cliquez sur l’icône de table avec la **+** (plus) sur celui-ci.</span><span class="sxs-lookup"><span data-stu-id="b714d-492">Click the table icon with the **+** (plus) on it.</span></span>

    ![Ajouter une nouvelle table](images/AzureLabs-Lab313-48.png)

7. <span data-ttu-id="b714d-494">Une fenêtre s’affiche invite pour pouvoir *ajouter une entité*.</span><span class="sxs-lookup"><span data-stu-id="b714d-494">A window will appear prompting for you to *Add Entity*.</span></span> <span data-ttu-id="b714d-495">Vous allez créer qu’une seule entité, s’il trois propriétés.</span><span class="sxs-lookup"><span data-stu-id="b714d-495">You will create only one entity, though it will have three properties.</span></span> <span data-ttu-id="b714d-496">Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournies, car elles sont utilisées par la table à rechercher vos données.</span><span class="sxs-lookup"><span data-stu-id="b714d-496">You will notice that *PartitionKey* and *RowKey* are already provided, as these are used by the table to find your data.</span></span> 

    ![clé de partition et de ligne](images/AzureLabs-Lab313-49.png)

8. <span data-ttu-id="b714d-498">Mettre à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b714d-498">Update the following values:</span></span>

    - <span data-ttu-id="b714d-499">Nom : **PartitionKey**, valeur : **PK_IoTMessages**</span><span class="sxs-lookup"><span data-stu-id="b714d-499">Name: **PartitionKey**, Value: **PK_IoTMessages**</span></span> 

    - <span data-ttu-id="b714d-500">Nom : **RowKey**, valeur : **RK_1_IoTMessages**</span><span class="sxs-lookup"><span data-stu-id="b714d-500">Name: **RowKey**, Value: **RK_1_IoTMessages**</span></span> 

9. <span data-ttu-id="b714d-501">Ensuite, cliquez sur **ajouter une propriété** (à l’angle inférieur gauche de la *ajouter une entité* fenêtre) et ajoutez la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="b714d-501">Then, click **Add property** (to the lower left of the *Add Entity* window) and add the following property:</span></span>

    - <span data-ttu-id="b714d-502">**Le MessageContent**, comme un *chaîne*, laissez la valeur vide.</span><span class="sxs-lookup"><span data-stu-id="b714d-502">**MessageContent**, as a *string*, leave the Value empty.</span></span>

10. <span data-ttu-id="b714d-503">Votre table doit correspondre à celui de l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b714d-503">Your table should match the one in the image below:</span></span>

    ![ajouter des valeurs correctes](images/AzureLabs-Lab313-50.png)

    > [!NOTE] 
    > <span data-ttu-id="b714d-505">La raison pour laquelle l’entité dispose le numéro 1 dans la clé de ligne, est, car vous souhaiterez peut-être ajouter plus de messages, vous souhaitez faire des essais avec ce cours.</span><span class="sxs-lookup"><span data-stu-id="b714d-505">The reason why the entity has the number 1 in the row key, is because you might want to add more messages, should you desire to experiment further with this course.</span></span>

11. <span data-ttu-id="b714d-506">Cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="b714d-506">Click **OK** when you are finished.</span></span> <span data-ttu-id="b714d-507">Votre table est maintenant prête à être utilisé.</span><span class="sxs-lookup"><span data-stu-id="b714d-507">Your table is now ready to be used.</span></span>

## <a name="chapter-13---create-an-azure-function-app"></a><span data-ttu-id="b714d-508">Chapitre 13 - créer une application de fonction Azure</span><span class="sxs-lookup"><span data-stu-id="b714d-508">Chapter 13 - Create an Azure Function App</span></span> 

<span data-ttu-id="b714d-509">Il est temps maintenant de créer un *Azure Function App*, qui sera appelé par le *Service IoT Hub* pour stocker le *IoT Edge* messages d’appareil dans le **Table** Service, que vous avez créé dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="b714d-509">It is now time to create an *Azure Function App*, which will be called by the *IoT Hub Service* to store the *IoT Edge* device messages in the **Table** Service, which you created in the previous Chapter.</span></span>

<span data-ttu-id="b714d-510">Vous devez tout d’abord, créez un fichier qui permettra à votre fonction Azure charger les bibliothèques que vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="b714d-510">First, you need to create a file that will allow your Azure Function to load the libraries you need.</span></span>

1.  <span data-ttu-id="b714d-511">Ouvrez **le bloc-notes** (appuyez sur la *Windows clé*et le type *le bloc-notes*).</span><span class="sxs-lookup"><span data-stu-id="b714d-511">Open **Notepad** (press the *Windows Key*, and type *notepad*).</span></span>

    ![Ouvrez le bloc-notes](images/AzureLabs-Lab313-51.png)

2.  <span data-ttu-id="b714d-513">Avec le bloc-notes ouvert, insérer la structure JSON ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b714d-513">With Notepad open, insert the JSON structure below into it.</span></span> <span data-ttu-id="b714d-514">Une fois que vous avez terminé, enregistrez-le sur votre bureau en tant que **project.json**.</span><span class="sxs-lookup"><span data-stu-id="b714d-514">Once you have done that, save it on your desktop as **project.json**.</span></span> <span data-ttu-id="b714d-515">Ce fichier définit les bibliothèques de que votre fonction utilisera.</span><span class="sxs-lookup"><span data-stu-id="b714d-515">This file defines the libraries your function will use.</span></span> <span data-ttu-id="b714d-516">Si vous avez utilisé NuGet, il vous sera familier.</span><span class="sxs-lookup"><span data-stu-id="b714d-516">If you have used NuGet, it will look familiar.</span></span>
    
    > [!WARNING]
    > <span data-ttu-id="b714d-517">Il est important que l’attribution de noms est correcte ; faire en sorte qu’il cas **n’a pas un .txt** extension de fichier.</span><span class="sxs-lookup"><span data-stu-id="b714d-517">It is important that the naming is correct; ensure it does **NOT have a .txt** file extension.</span></span> <span data-ttu-id="b714d-518">Pour référence, voir ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b714d-518">See below for reference:</span></span>
    >
    > ![Enregistrement JSON](images/AzureLabs-Lab313-52.png)

    ```json
    {
    "frameworks": {
        "net46":{
        "dependencies": {
            "WindowsAzure.Storage": "9.2.0"
        }
        }
    }
    }
    ```

3.  <span data-ttu-id="b714d-520">Connectez-vous à la [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b714d-520">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

4.  <span data-ttu-id="b714d-521">Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche coin inférieur droit, puis recherchez **Function App**, puis appuyez sur la **entrée** clé, à rechercher.</span><span class="sxs-lookup"><span data-stu-id="b714d-521">Once you are logged in, click on **Create a resource** in the top left corner, and search for **Function App**, and press the **Enter** key, to search.</span></span> <span data-ttu-id="b714d-522">Cliquez sur *Function App* dans les résultats, pour ouvrir un nouveau volet.</span><span class="sxs-lookup"><span data-stu-id="b714d-522">Click *Function App* from the results, to open a new panel.</span></span>

    ![recherche de l’application de fonction](images/AzureLabs-Lab313-53.png)

5.  <span data-ttu-id="b714d-524">Le nouveau panneau fournit une description de la **Function App** Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-524">The new panel will provide a description of the **Function App** Service.</span></span> <span data-ttu-id="b714d-525">En bas à gauche de ce panneau, cliquez sur le **créer** bouton, pour créer une association avec ce Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-525">At the bottom left of this panel, click the **Create** button, to create an association with this Service.</span></span>

    ![instance d’application (fonction)](images/AzureLabs-Lab313-54.png)

6.  <span data-ttu-id="b714d-527">Une fois que vous avez cliqué sur **créer**, renseignez les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="b714d-527">Once you have clicked on **Create**, fill in the following:</span></span>

    1. <span data-ttu-id="b714d-528">Pour **nom de l’application**, insérez votre nom souhaité pour cette instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-528">For **App name**, insert your desired name for this Service instance.</span></span>

    2. <span data-ttu-id="b714d-529">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="b714d-529">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="b714d-530">Sélectionnez le niveau de tarification approprié pour vous, si c’est la première heure de création d’un **Service Function App**, un niveau gratuit doit être disponible pour vous.</span><span class="sxs-lookup"><span data-stu-id="b714d-530">Select the pricing tier appropriate for you, if this is the first time creating a **Function App Service**, a free tier should be available to you.</span></span>

    4. <span data-ttu-id="b714d-531">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="b714d-531">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="b714d-532">Un groupe de ressources offre un moyen pour surveiller, de contrôler l’accès, disposition et de gérer, de facturation pour une collection de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="b714d-532">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="b714d-533">Il est recommandé de garder tous les Services Azure associés à un projet unique (par exemple, par exemple, ces cours) sous un groupe de ressources communs).</span><span class="sxs-lookup"><span data-stu-id="b714d-533">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="b714d-534">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, veuillez suivre ce [lien sur la façon de gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="b714d-534">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="b714d-535">Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme.</span><span class="sxs-lookup"><span data-stu-id="b714d-535">For **OS**, click Windows, as that is the intended platform.</span></span>

    6. <span data-ttu-id="b714d-536">Sélectionnez un **Plan d’hébergement** (à l’aide de ce didacticiel est un **Plan de consommation**.</span><span class="sxs-lookup"><span data-stu-id="b714d-536">Select a **Hosting Plan** (this tutorial is using a **Consumption Plan**.</span></span>

    7. <span data-ttu-id="b714d-537">Sélectionnez un **emplacement** (choisissez le même emplacement que le stockage que vous avez créé à l’étape précédente)</span><span class="sxs-lookup"><span data-stu-id="b714d-537">Select a **Location** (choose the same location as the storage you have built in the previous step)</span></span>

    8. <span data-ttu-id="b714d-538">Pour le **stockage** section, **vous devez sélectionner le Service de stockage que vous avez créé à l’étape précédente**.</span><span class="sxs-lookup"><span data-stu-id="b714d-538">For the **Storage** section, **you must select the Storage Service you created in the previous step**.</span></span>

    9. <span data-ttu-id="b714d-539">Vous n’aurez pas *Application Insights* dans cette application, par conséquent, n’hésitez pas à laisser **hors**.</span><span class="sxs-lookup"><span data-stu-id="b714d-539">You will not need *Application Insights* in this app, so feel free to leave it **Off**.</span></span>

    10. <span data-ttu-id="b714d-540">Cliquez sur **Create (Créer)**.</span><span class="sxs-lookup"><span data-stu-id="b714d-540">Click **Create**.</span></span>

        ![créer la nouvelle instance](images/AzureLabs-Lab313-55.png)

7.  <span data-ttu-id="b714d-542">Une fois que vous avez cliqué sur **créer**, vous devrez attendre que le Service doit être créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="b714d-542">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

8.  <span data-ttu-id="b714d-543">Une fois que l’instance de Service est créée, une notification s’affiche dans le portail.</span><span class="sxs-lookup"><span data-stu-id="b714d-543">A notification will appear in the Portal once the Service instance is created.</span></span>

    ![nouvelle notification](images/AzureLabs-Lab313-56.png)

9.  <span data-ttu-id="b714d-545">Cliquez sur la notification, une fois que le déploiement a réussi (terminée).</span><span class="sxs-lookup"><span data-stu-id="b714d-545">Click on the notification, once deployment is successful (has finished).</span></span>

10. <span data-ttu-id="b714d-546">Cliquez sur le **accéder à la ressource** bouton dans la notification pour Explorer votre nouvelle instance de Service.</span><span class="sxs-lookup"><span data-stu-id="b714d-546">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> 

    ![accéder à la ressource](images/AzureLabs-Lab313-57.png)

11. <span data-ttu-id="b714d-548">Dans la partie gauche du panneau Nouveau, cliquez sur le **+** (plus) de l’icône située à côté *fonctions*, pour créer une nouvelle fonction.</span><span class="sxs-lookup"><span data-stu-id="b714d-548">In the left side of the new panel, click the **+** (plus) icon next to *Functions*, to create a new function.</span></span>

    ![ajouter la nouvelle fonction](images/AzureLabs-Lab313-58.png)

12. <span data-ttu-id="b714d-550">Dans le volet central, le **fonction** fenêtre de création s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b714d-550">Within the central panel, the **Function** creation window will appear.</span></span> <span data-ttu-id="b714d-551">Descendez plus bas, puis cliquez sur **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="b714d-551">Scroll down further, and click on **Custom function**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-59.png)

13. <span data-ttu-id="b714d-553">Défilement vers le bas de la page suivante, jusqu'à ce que vous trouviez **IoT Hub (Event Hub)**, puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="b714d-553">Scroll down the next page, until you find **IoT Hub (Event Hub)**, then click on it.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-60.png)

14. <span data-ttu-id="b714d-555">Dans le **IoT Hub (Event Hub)** panneau, définissez la **langage** à **C#** , puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="b714d-555">In the **IoT Hub (Event Hub)** blade, set the **Language** to **C#** and then click on **new**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-61.png)

15. <span data-ttu-id="b714d-557">Dans la fenêtre qui s’affiche, assurez-vous que **IoT Hub** est sélectionné et le nom de la *IoT Hub* champ correspond au nom de votre *Service IoT Hub* que vous avez créé précédemment ([à l’étape 8, du chapitre 3](#chapter-3---the-iot-hub-service)).</span><span class="sxs-lookup"><span data-stu-id="b714d-557">In the window that will appear, make sure that **IoT Hub** is selected and the name of the *IoT Hub* field corresponds with the name of your *IoT Hub Service* that you have created previously ([in step 8, of Chapter 3](#chapter-3---the-iot-hub-service)).</span></span> <span data-ttu-id="b714d-558">Puis cliquez sur le **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="b714d-558">Then click the **Select** button.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-62.png)

16. <span data-ttu-id="b714d-560">Sur le **IoT Hub (Event Hub)** panneau, cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-560">Back on the **IoT Hub (Event Hub)** blade, click on **Create**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-63.png)

17. <span data-ttu-id="b714d-562">Vous êtes redirigé vers l’éditeur de fonction.</span><span class="sxs-lookup"><span data-stu-id="b714d-562">You will be redirected to the function editor.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-64.png)

18. <span data-ttu-id="b714d-564">Supprimez tout le code qu’il contient et remplacez-le par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="b714d-564">Delete all the code in it and replace it with the following:</span></span>

    ```csharp
    #r "Microsoft.WindowsAzure.Storage"
    #r "NewtonSoft.Json"

    using System;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Table;
    using Newtonsoft.Json;
    using System.Threading.Tasks;

    public static async Task Run(string myIoTHubMessage, TraceWriter log)
    {
        log.Info($"C# IoT Hub trigger function processed a message: {myIoTHubMessage}");
        
        //RowKey of the table object to be changed
        string tableName = "IoTMessages";
        string tableURL = "https://iothubmrstorage.table.core.windows.net/IoTMessages";

        // If you did not name your Storage Service as suggested in the course, change the name here with the one you chose.
        string storageAccountName = "iotedgestor"; 

        string storageAccountKey = "<Insert your Storage Key here>";   

        string partitionKey = "PK_IoTMessages";
        string rowKey = "RK_1_IoTMessages";

        Microsoft.WindowsAzure.Storage.Auth.StorageCredentials storageCredentials =
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(storageAccountName, storageAccountKey);

        CloudStorageAccount storageAccount = new CloudStorageAccount(storageCredentials, true);

        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

        // Get a reference to a table named "IoTMessages"
        CloudTable messageTable = tableClient.GetTableReference(tableName);

        //Retrieve the table object by its RowKey
        TableOperation operation = TableOperation.Retrieve<MessageEntity>(partitionKey, rowKey);
        TableResult result = await messageTable.ExecuteAsync(operation);

        //Create a MessageEntity so to set its parameters
        MessageEntity messageEntity = (MessageEntity)result.Result;

        messageEntity.MessageContent = myIoTHubMessage;
        messageEntity.PartitionKey = partitionKey;
        messageEntity.RowKey = rowKey;

        //Replace the table appropriate table Entity with the value of the MessageEntity Ccass structure.
        operation = TableOperation.Replace(messageEntity);

        // Execute the insert operation.
        await messageTable.ExecuteAsync(operation);
    }

    // This MessageEntity structure which will represent a Table Entity
    public class MessageEntity : TableEntity
    {
        public string Type { get; set; }
        public string MessageContent { get; set; }   
    }
    ```

19. <span data-ttu-id="b714d-565">Modifier les variables suivantes, afin qu’ils correspondent aux valeurs appropriées (**Table** et **stockage** valeurs, à partir de [l’étape 11 et 13, respectivement, du chapitre 11](#chapter-11---create-table-service)), que vous rencontrerez dans vos **compte de stockage**:</span><span class="sxs-lookup"><span data-stu-id="b714d-565">Change the following variables, so that they correspond to the appropriate values (**Table** and **Storage** values, from [step 11 and 13, respectively, of Chapter 11](#chapter-11---create-table-service)), that you will find in your **Storage Account**:</span></span>

    - <span data-ttu-id="b714d-566">**tableName**, avec le nom de votre **Table** situé dans votre **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="b714d-566">**tableName**, with the name of your **Table** located in your **Storage Account**.</span></span>
    - <span data-ttu-id="b714d-567">**tableURL**, avec l’URL de votre **Table** situé dans votre **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="b714d-567">**tableURL**, with the URL of your **Table** located in your **Storage Account**.</span></span>
    - <span data-ttu-id="b714d-568">**storageAccountName**, avec le nom de la valeur correspondant avec le nom de votre **compte de stockage** nom.</span><span class="sxs-lookup"><span data-stu-id="b714d-568">**storageAccountName**, with the name of the value corresponding with the name of your **Storage Account** name.</span></span>
    - <span data-ttu-id="b714d-569">**storageAccountKey**, avec la clé que vous avez obtenu dans le Service de stockage que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b714d-569">**storageAccountKey**, with the Key you have obtained in the Storage Service you have created previously.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-65.png)

20. <span data-ttu-id="b714d-571">Le code en place, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-571">With the code in place, click **Save**.</span></span>

21. <span data-ttu-id="b714d-572">Ensuite, cliquez sur le **\<** icône (flèche), sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="b714d-572">Next, click the **\<** (arrow) icon, on the right-hand side of the page.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-66.png)

22. <span data-ttu-id="b714d-574">Un glisser en partant de la droite.</span><span class="sxs-lookup"><span data-stu-id="b714d-574">A panel will slide in from the right.</span></span> <span data-ttu-id="b714d-575">Dans ce panneau, cliquez sur **télécharger**et un *Explorateur de fichiers* s’affiche.</span><span class="sxs-lookup"><span data-stu-id="b714d-575">In that panel, click **Upload**, and a *File Browser* will appear.</span></span>

23. <span data-ttu-id="b714d-576">Accédez à, puis cliquez sur, la **project.json** fichier que vous avez créé dans **le bloc-notes** précédemment, puis cliquez sur le **Open** bouton.</span><span class="sxs-lookup"><span data-stu-id="b714d-576">Navigate to, and click, the **project.json** file, which you created in **Notepad** previously, and then click the **Open** button.</span></span> <span data-ttu-id="b714d-577">Ce fichier définit les bibliothèques utilisées par votre fonction.</span><span class="sxs-lookup"><span data-stu-id="b714d-577">This file defines the libraries that your function will use.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-67.png)

24. <span data-ttu-id="b714d-579">Quand le fichier a été chargé, il apparaît dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="b714d-579">When the file has uploaded, it will appear in the panel on the right.</span></span> <span data-ttu-id="b714d-580">En cliquant sur il s’ouvre dans le **fonction** éditeur.</span><span class="sxs-lookup"><span data-stu-id="b714d-580">Clicking it will open it within the **Function** editor.</span></span> <span data-ttu-id="b714d-581">Il doit rechercher **exactement** identique à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="b714d-581">It must look **exactly** the same as the next image.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-68.png)

25. <span data-ttu-id="b714d-583">À ce stade il serait judicieux de tester la fonction de votre fonction pour stocker le message sur votre *Table*.</span><span class="sxs-lookup"><span data-stu-id="b714d-583">At this point it would be good to test the capability of your Function to store the message on your *Table*.</span></span> <span data-ttu-id="b714d-584">Sur le côté droit de la fenêtre, cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="b714d-584">On the top right side of the window, click on **Test**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-69.png)

26. <span data-ttu-id="b714d-586">Insérer un message sur le **corps de la demande**, comme illustré dans l’image ci-dessus, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="b714d-586">Insert a message on the **Request body**, as shown in the image above, and click on **Run**.</span></span> 

27. <span data-ttu-id="b714d-587">La fonction s’exécute, en affichant l’état de résultat (vous remarquerez le vert **état 202 accepté**, ci-dessus le *sortie* fenêtre, ce qui signifie qu’il a un appel réussi) :</span><span class="sxs-lookup"><span data-stu-id="b714d-587">The function will run, displaying the result status (you will notice the green **Status 202 Accepted**, above the *Output* window, which means it was a successful call):</span></span>

    ![résultat de sortie](images/AzureLabs-Lab313-70.png)

## <a name="chapter-14---view-active-messages"></a><span data-ttu-id="b714d-589">Chapitre 14 - afficher les messages actives</span><span class="sxs-lookup"><span data-stu-id="b714d-589">Chapter 14 - View active messages</span></span>

<span data-ttu-id="b714d-590">Si vous ouvrez Visual Studio (**pas** Visual Studio Code), vous pouvez visualiser les résultats de votre message test, tel qu’il sera stocké dans le *le MessageContent* zone de chaîne.</span><span class="sxs-lookup"><span data-stu-id="b714d-590">If you now open Visual Studio (**not** Visual Studio Code), you can visualize your test message result, as it will be stored in the *MessageContent* string area.</span></span>

![fonction personnalisée](images/AzureLabs-Lab313-71.png)

<span data-ttu-id="b714d-592">Avec le Service de Table et l’application de fonction en place, les messages de votre appareil Ubuntu seront affichera dans votre *IoTMessages* Table.</span><span class="sxs-lookup"><span data-stu-id="b714d-592">With the Table Service and Function App in place, your Ubuntu device messages will appear in your *IoTMessages* Table.</span></span> <span data-ttu-id="b714d-593">Si pas déjà en cours d’exécution, redémarrez votre appareil et vous serez en mesure de voir les messages de résultat à partir de votre appareil et le module, au sein de votre Table, l’aide de Visual Studio *Cloud Explorer*.</span><span class="sxs-lookup"><span data-stu-id="b714d-593">If not already running, start your device again, and you will be able to see the result messages from your device, and module, within your Table, through using Visual Studio *Cloud Explorer*.</span></span>

![Visualiser les données](images/AzureLabs-Lab313-72.png)


## <a name="chapter-15---power-bi-setup"></a><span data-ttu-id="b714d-595">Chapitre 15 - le programme d’installation de Power BI</span><span class="sxs-lookup"><span data-stu-id="b714d-595">Chapter 15 - Power BI Setup</span></span>

<span data-ttu-id="b714d-596">Pour visualiser les données à partir de votre appareil IOT vous permettra de configurer **Power BI** (version de bureau), pour collecter les données à partir de la *Table* Service, qui vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="b714d-596">To visualize the data from your IOT device you will setup **Power BI** (desktop version), to collect the data from the *Table* Service, which you just created.</span></span> <span data-ttu-id="b714d-597">Le *HoloLens* version de Power BI utiliserez ensuite ces données pour visualiser le résultat.</span><span class="sxs-lookup"><span data-stu-id="b714d-597">The *HoloLens* version of Power BI will then use that data to visualize the result.</span></span>

1.  <span data-ttu-id="b714d-598">Ouvrez le Microsoft Store sur Windows 10 et recherchez **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="b714d-598">Open the Microsoft Store on Windows 10 and search for **Power BI Desktop**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-73.png)

2.  <span data-ttu-id="b714d-600">Télécharger l’application.</span><span class="sxs-lookup"><span data-stu-id="b714d-600">Download the application.</span></span> <span data-ttu-id="b714d-601">Une fois le téléchargement terminé, l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="b714d-601">Once it has finished downloading, open it.</span></span>

3.  <span data-ttu-id="b714d-602">Connectez-vous à *Power BI* avec votre **compte Microsoft 365**.</span><span class="sxs-lookup"><span data-stu-id="b714d-602">Log into *Power BI* with your **Microsoft 365 account**.</span></span> <span data-ttu-id="b714d-603">Vous pouvez être redirigé vers un navigateur, pour vous inscrire.</span><span class="sxs-lookup"><span data-stu-id="b714d-603">You may be redirected to a browser, to sign up.</span></span> <span data-ttu-id="b714d-604">Une fois que vous êtes inscrit, revenez à l’application Power BI et vous reconnecter.</span><span class="sxs-lookup"><span data-stu-id="b714d-604">Once you are signed up, go back to the Power BI app, and sign in again.</span></span>

4.  <span data-ttu-id="b714d-605">Cliquez sur **obtenir des données** , puis cliquez sur **plus...** .</span><span class="sxs-lookup"><span data-stu-id="b714d-605">Click on **Get Data** and then click on **More...**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-74.png)

5.  <span data-ttu-id="b714d-607">Cliquez sur **Azure**, **stockage Table Azure**, puis cliquez sur **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b714d-607">Click **Azure**, **Azure Table Storage**, then click on **Connect**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-75.png)

6.  <span data-ttu-id="b714d-609">Vous devrez insérer le **Table URL** que vous avez collectées précédemment ([à l’étape 13 du chapitre 11](#chapter-11---create-table-service)), lors de la création de votre Service de Table.</span><span class="sxs-lookup"><span data-stu-id="b714d-609">You will be prompted to insert the **Table URL** that you collected earlier ([in step 13 of Chapter 11](#chapter-11---create-table-service)), while creating your Table Service.</span></span> <span data-ttu-id="b714d-610">Après avoir inséré l’URL, supprimez la portion du chemin d’accès faisant référence à la Table « sous-dossier » (qui était IoTMessages, dans ce cours).</span><span class="sxs-lookup"><span data-stu-id="b714d-610">After inserting the URL, delete the portion of the path referring to the Table "sub-folder" (which was IoTMessages, in this course).</span></span> <span data-ttu-id="b714d-611">Le résultat final doit être tel qu’affiché dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b714d-611">The final result should be as displayed in the image below.</span></span> <span data-ttu-id="b714d-612">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b714d-612">Then click on **OK**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-76.png)

7.  <span data-ttu-id="b714d-614">Vous devrez insérer le **clé de stockage** que vous avez notée ([à l’étape 11 du chapitre 11](#chapter-11---create-table-service)) antérieures lors de la création de votre stockage Table.</span><span class="sxs-lookup"><span data-stu-id="b714d-614">You will be prompted to insert the **Storage Key** that you noted ([in step 11 of Chapter 11](#chapter-11---create-table-service)) earlier while creating your Table Storage.</span></span> <span data-ttu-id="b714d-615">Cliquez ensuite sur **Connect**.</span><span class="sxs-lookup"><span data-stu-id="b714d-615">Then click on **Connect**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-77.png)  

8. <span data-ttu-id="b714d-617">Un **panneau navigation** s’affiche, cochez la case en regard de votre Table et cliquez sur **charge**.</span><span class="sxs-lookup"><span data-stu-id="b714d-617">A **Navigator Panel** will be displayed, tick the box next to your Table and click on **Load**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-78.png)  

9. <span data-ttu-id="b714d-619">Votre table a maintenant été chargée sur Power BI, mais elle nécessite une requête pour afficher les valeurs qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="b714d-619">Your table has now been loaded on Power BI, but it requires a query to display the values in it.</span></span> <span data-ttu-id="b714d-620">Pour ce faire, cliquez sur le nom de la table situé dans le **panneau champs** sur le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="b714d-620">To do so, right-click on the table name located in the **FIELDS panel** at the right side of the screen.</span></span> <span data-ttu-id="b714d-621">Cliquez ensuite sur **modifier la requête**.</span><span class="sxs-lookup"><span data-stu-id="b714d-621">Then click on **Edit Query**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-79.png) 

10. <span data-ttu-id="b714d-623">Un **Power Query Editor** ouvrira une nouvelle fenêtre, affichage de votre table.</span><span class="sxs-lookup"><span data-stu-id="b714d-623">A **Power Query Editor**  will open up as a new window, displaying your table.</span></span> <span data-ttu-id="b714d-624">Cliquez sur le mot **enregistrement** au sein de la *contenu* colonne de la table, pour visualiser votre contenu stocké.</span><span class="sxs-lookup"><span data-stu-id="b714d-624">Click on the word **Record** within the *Content* column of the table, to visualize your stored content.</span></span>

    ![Power BI](images/AzureLabs-Lab313-80.png)    

11. <span data-ttu-id="b714d-626">Cliquez sur **dans la Table**, à l’angle supérieur gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b714d-626">Click on **Into Table**, at the top-left of the window.</span></span> 

    ![Power BI](images/AzureLabs-Lab313-81.png)

12. <span data-ttu-id="b714d-628">Cliquez sur **Fermer & appliquer**.</span><span class="sxs-lookup"><span data-stu-id="b714d-628">Click on **Close & Apply**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-82.png)

13. <span data-ttu-id="b714d-630">Une fois qu’il a terminé de charger la requête, dans le **panneau champs**, sur le côté droit de l’écran, cochez les cases à cocher correspondant aux paramètres **nom** et **valeur**, à visualiser le **le MessageContent** contenu de la colonne.</span><span class="sxs-lookup"><span data-stu-id="b714d-630">Once it has finished loading the query, within the **FIELDS panel**, on the right side of the screen, tick the boxes corresponding to the parameters **Name** and **Value**, to visualize the **MessageContent** column content.</span></span>

    ![Power BI](images/AzureLabs-Lab313-83.png)

14. <span data-ttu-id="b714d-632">Cliquez sur le **icône de disque bleu** en haut à gauche de la fenêtre pour enregistrer votre travail dans un dossier de votre choix.</span><span class="sxs-lookup"><span data-stu-id="b714d-632">Click on the **blue disk icon** at the top left of the window to save your work in a folder of your choice.</span></span>

    ![Power BI](images/AzureLabs-Lab313-84.png)

15. <span data-ttu-id="b714d-634">Vous pouvez maintenant cliquer sur le bouton Publier pour charger votre table dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="b714d-634">You can now click on the Publish button to upload your table to your Workspace.</span></span> <span data-ttu-id="b714d-635">Lorsque vous y êtes invité, cliquez sur **mon espace de travail** et cliquez sur *sélectionnez*.</span><span class="sxs-lookup"><span data-stu-id="b714d-635">When prompted, click **My workspace** and click *Select*.</span></span> <span data-ttu-id="b714d-636">Attendez qu’elle afficher le résultat de réussite de l’envoi.</span><span class="sxs-lookup"><span data-stu-id="b714d-636">Wait for it to display the successful result of the submission.</span></span>

    ![Power BI](images/AzureLabs-Lab313-85.png)

    ![Power BI](images/AzureLabs-Lab313-86.png)

> [!WARNING]
> <span data-ttu-id="b714d-639">Le chapitre suivant est HoloLens spécifique.</span><span class="sxs-lookup"><span data-stu-id="b714d-639">The following Chapter is HoloLens specific.</span></span> <span data-ttu-id="b714d-640">Power BI n’est pas actuellement disponible en tant qu’une application, mais vous pouvez exécuter la version de bureau dans le portail de réalité mixte Windows (également appelé Cliff House), via l’application de bureau.</span><span class="sxs-lookup"><span data-stu-id="b714d-640">Power BI is not currently availble as an immersive application, however you can run the desktop version in the Windows Mixed Reality Portal (aka Cliff House), through the Desktop app.</span></span>

## <a name="chapter-16---display-power-bi-data-on-hololens"></a><span data-ttu-id="b714d-641">Chapitre 16 - données d’affichage Power BI sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="b714d-641">Chapter 16 - Display Power BI data on HoloLens</span></span>

1. <span data-ttu-id="b714d-642">Sur votre HoloLens, connectez-vous à la **Microsoft Store**, en appuyant sur son icône dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="b714d-642">On your HoloLens, log in to the **Microsoft Store**, by tapping on its icon in the applications list.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-87.png)

2. <span data-ttu-id="b714d-644">Recherchez et téléchargez ensuite le **Power BI** application.</span><span class="sxs-lookup"><span data-stu-id="b714d-644">Search and then download the **Power BI** application.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-88.png)

3. <span data-ttu-id="b714d-646">Démarrer **Power BI** à partir de votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="b714d-646">Start **Power BI** from your applications list.</span></span> 

4. <span data-ttu-id="b714d-647">**Power BI** peut vous demander de se connecter à votre **compte Microsoft 365**.</span><span class="sxs-lookup"><span data-stu-id="b714d-647">**Power BI** might ask you to login to your **Microsoft 365 account**.</span></span>

5. <span data-ttu-id="b714d-648">Une fois à l’intérieur de l’application, l’espace de travail doit afficher par défaut comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b714d-648">Once inside the app, the workspace should display by default as shown in the image below.</span></span> <span data-ttu-id="b714d-649">Si qui ne se produit pas, cliquez simplement sur l’icône de l’espace de travail sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="b714d-649">If that does not happen, simply click on the workspace icon on the left side of the window.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-89.png)

## <a name="your-finished-your-iot-hub-application"></a><span data-ttu-id="b714d-651">Votre application de votre IoT Hub terminée</span><span class="sxs-lookup"><span data-stu-id="b714d-651">Your finished your IoT Hub application</span></span>

<span data-ttu-id="b714d-652">Félicitations, vous avez créé un Service IoT Hub, avec un appareil simulé Edge de la Machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="b714d-652">Congratulations, you have successfully created an IoT Hub Service, with a simulated Virtual Machine Edge device.</span></span> <span data-ttu-id="b714d-653">Votre appareil peut communiquer les résultats d’un modèle machine learning à un Service de Table Azure, facilité par une application de fonction Azure, qui est lu dans Power BI et visualisées dans un Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b714d-653">Your device can  communicate the results of a machine learning model to an Azure Table Service, facilitated by an Azure Function App, which is read into Power BI, and visualized within a Microsoft HoloLens.</span></span>
 
![Power BI](images/AzureLabs-Lab313-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="b714d-655">Exercices de bonus</span><span class="sxs-lookup"><span data-stu-id="b714d-655">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="b714d-656">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="b714d-656">Exercise 1</span></span>

<span data-ttu-id="b714d-657">Développez la structure de messagerie stockée dans la table et l’afficher sous forme de graphique.</span><span class="sxs-lookup"><span data-stu-id="b714d-657">Expand the messaging structure stored in the table and display it as a graph.</span></span> <span data-ttu-id="b714d-658">Vous souhaiterez peut-être collecter davantage de données et les stocker dans la même table, pour être affiché ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="b714d-658">You might want to collect more data and store it in the same table, to be later displayed.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="b714d-659">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="b714d-659">Exercise 2</span></span>

<span data-ttu-id="b714d-660">Créer un autre module « capture de l’appareil photo » doit être déployé sur le tableau IoT, afin qu’il peut capturer des images via l’appareil photo à analyser.</span><span class="sxs-lookup"><span data-stu-id="b714d-660">Create an additional "camera capture" module to be deployed on the IoT board, so that it can capture images through the camera to be analyzed.</span></span>
