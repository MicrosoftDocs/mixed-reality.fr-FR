---
title: RM et Azure 313-IoT Hub service
description: Suivez ce cours pour apprendre à implémenter Azure IoT Hub service sur une machine virtuelle exécutant Ubuntu 16,4, puis visualisez les données de message à l’aide de Microsoft HoloLens ou d’un casque immersif.
author: drneil
ms.author: jemccull
ms.date: 07/11/2018
ms.topic: article
keywords: Azure, réalité mixte, Académie, périphérie, IOT Edge, didacticiel, API, notification, fonctions, tables, hololens, immersif, VR, IOT, machine virtuelle, Ubuntu, Python
ms.openlocfilehash: bfb1518869892ed4899019d7b9c504a960e7db3f
ms.sourcegitcommit: 2cf3f19146d6a7ba71bbc4697a59064b4822b539
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/12/2019
ms.locfileid: "73926837"
---
>[!NOTE]
><span data-ttu-id="0035a-104">Les didacticiels d’Académie de la réalité mixte ont été conçus avec les casques immersif (1er génération) et de réalité mixte à l’esprit.</span><span class="sxs-lookup"><span data-stu-id="0035a-104">The Mixed Reality Academy tutorials were designed with HoloLens (1st gen) and Mixed Reality Immersive Headsets in mind.</span></span>  <span data-ttu-id="0035a-105">Par conséquent, nous pensons qu’il est important de ne pas mettre en place ces didacticiels pour les développeurs qui cherchent toujours des conseils en matière de développement pour ces appareils.</span><span class="sxs-lookup"><span data-stu-id="0035a-105">As such, we feel it is important to leave these tutorials in place for developers who are still looking for guidance in developing for those devices.</span></span>  <span data-ttu-id="0035a-106">Ces didacticiels ne seront **_pas_** mis à jour avec les derniers ensembles d’outils ou interactions utilisés pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="0035a-106">These tutorials will **_not_** be updated with the latest toolsets or interactions being used for HoloLens 2.</span></span>  <span data-ttu-id="0035a-107">Ils seront conservés pour continuer à travailler sur les appareils pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0035a-107">They will be maintained to continue working on the supported devices.</span></span> <span data-ttu-id="0035a-108">Une nouvelle série de didacticiels sera publiée à l’avenir qui vous montrera comment développer pour HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="0035a-108">There will be a new series of tutorials that will be posted in the future that will demonstrate how to develop for HoloLens 2.</span></span>  <span data-ttu-id="0035a-109">Cet avis sera mis à jour avec un lien vers ces didacticiels lors de leur publication.</span><span class="sxs-lookup"><span data-stu-id="0035a-109">This notice will be updated with a link to those tutorials when they are posted.</span></span>

# <a name="mr-and-azure-313-iot-hub-service"></a><span data-ttu-id="0035a-110">MR et Azure 313 : service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0035a-110">MR and Azure 313: IoT Hub Service</span></span>

![résultat du cours](images/AzureLabs-Lab313-00.png)

<span data-ttu-id="0035a-112">Dans ce cours, vous allez apprendre à implémenter un **service Azure IOT Hub** sur une machine virtuelle exécutant le système d’exploitation Ubuntu 16,4.</span><span class="sxs-lookup"><span data-stu-id="0035a-112">In this course, you will learn how to implement an **Azure IoT Hub Service** on a virtual machine running the Ubuntu 16.4 operating system.</span></span> <span data-ttu-id="0035a-113">Un **Function App Azure** est ensuite utilisé pour recevoir des messages de votre machine virtuelle Ubuntu et stocker le résultat dans un **service de table Azure**.</span><span class="sxs-lookup"><span data-stu-id="0035a-113">An **Azure Function App** will then be used to receive messages from your Ubuntu VM, and store the result within an **Azure Table Service**.</span></span> <span data-ttu-id="0035a-114">Vous pourrez ensuite afficher ces données à l’aide de **Power bi** sur Microsoft HoloLens ou un casque immersif (VR).</span><span class="sxs-lookup"><span data-stu-id="0035a-114">You will then be able to view this data using **Power BI** on Microsoft HoloLens or immersive (VR) headset.</span></span>

<span data-ttu-id="0035a-115">Le contenu de ce cours *s’applique* aux appareils IOT Edge, bien que dans le cadre de ce cours, l’objectif est de se concentrer sur un environnement de machine virtuelle, de sorte que l’accès à un appareil de périphérie physique n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0035a-115">The content of this course *is applicable* to IoT Edge devices, though for the purpose of this course, the focus will be on a virtual machine environment, so that access to a physical Edge device is not necessary.</span></span>

<span data-ttu-id="0035a-116">En suivant ce cours, vous allez apprendre à :</span><span class="sxs-lookup"><span data-stu-id="0035a-116">By completing this course, you will learn to:</span></span>

- <span data-ttu-id="0035a-117">Déployez un **module IOT Edge** sur une machine virtuelle (Ubuntu 16 OS) qui représente votre appareil IOT.</span><span class="sxs-lookup"><span data-stu-id="0035a-117">Deploy an **IoT Edge module** to a Virtual Machine (Ubuntu 16 OS), which will represent your IoT device.</span></span>
- <span data-ttu-id="0035a-118">Ajoutez un **modèle Tensorflow Azure Custom vision** au module Edge, avec le code qui analysera les images stockées dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="0035a-118">Add an **Azure Custom Vision Tensorflow Model** to the Edge module, with code that will analyze images stored in the container.</span></span>
- <span data-ttu-id="0035a-119">Configurez le module pour renvoyer le message de résultat de l’analyse à votre **service de IOT Hub**.</span><span class="sxs-lookup"><span data-stu-id="0035a-119">Set up the module to send the analysis result message back to your **IoT Hub Service**.</span></span>
- <span data-ttu-id="0035a-120">Utilisez un **Function App Azure** pour stocker le message dans une **table Azure**.</span><span class="sxs-lookup"><span data-stu-id="0035a-120">Use an **Azure Function App** to store the message within an **Azure Table**.</span></span>
- <span data-ttu-id="0035a-121">Configurez **Power bi** pour collecter le message stocké et créer un rapport.</span><span class="sxs-lookup"><span data-stu-id="0035a-121">Set up **Power BI** to collect the stored message and create a report.</span></span>
- <span data-ttu-id="0035a-122">Visualisez les données de vos messages IoT dans **Power bi**.</span><span class="sxs-lookup"><span data-stu-id="0035a-122">Visualize your IoT message data within **Power BI**.</span></span>

<span data-ttu-id="0035a-123">Les services que vous allez utiliser sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="0035a-123">The Services you will use include:</span></span>

- <span data-ttu-id="0035a-124">**Azure IOT Hub** est un service Microsoft Azure qui permet aux développeurs de connecter, surveiller et gérer des ressources IOT.</span><span class="sxs-lookup"><span data-stu-id="0035a-124">**Azure IoT Hub** is a Microsoft Azure Service which allows developers to connect, monitor, and manage, IoT assets.</span></span> <span data-ttu-id="0035a-125">Pour plus d’informations, consultez la page du [ **Service Azure IOT Hub** ](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="0035a-125">For more information, visit the [**Azure IoT Hub Service** page](https://azure.microsoft.com/services/iot-hub/).</span></span>

- <span data-ttu-id="0035a-126">**Azure Container Registry** est un service Microsoft Azure qui permet aux développeurs de stocker des images de conteneur pour différents types de conteneurs.</span><span class="sxs-lookup"><span data-stu-id="0035a-126">**Azure Container Registry** is a Microsoft Azure Service which allows developers to store container images, for various types of containers.</span></span> <span data-ttu-id="0035a-127">Pour plus d’informations, consultez la page du [ **service Azure Container Registry** ](https://azure.microsoft.com/services/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="0035a-127">For more information, visit the [**Azure Container Registry Service** page](https://azure.microsoft.com/services/container-registry/).</span></span>

- <span data-ttu-id="0035a-128">**Azure Function App** est un service Microsoft Azure, qui permet aux développeurs d’exécuter de petits morceaux de code, « functions », dans Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-128">**Azure Function App** is a Microsoft Azure Service, which allows developers to run small pieces of code, 'functions', in Azure.</span></span> <span data-ttu-id="0035a-129">Cela permet de déléguer le travail au Cloud, plutôt qu’à votre application locale, ce qui peut avoir de nombreux avantages.</span><span class="sxs-lookup"><span data-stu-id="0035a-129">This provides a way to delegate work to the cloud, rather than your local application, which can have many benefits.</span></span> <span data-ttu-id="0035a-130">**Azure Functions** prend en charge plusieurs langages de développement, notamment C\#, F\#, node. js, Java et php.</span><span class="sxs-lookup"><span data-stu-id="0035a-130">**Azure Functions** supports several development languages, including C\#, F\#, Node.js, Java, and PHP.</span></span> <span data-ttu-id="0035a-131">Pour plus d’informations, consultez la [page **Azure Functions** ](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span><span class="sxs-lookup"><span data-stu-id="0035a-131">For more information, visit the [**Azure Functions** page](https://docs.microsoft.com/azure/azure-functions/functions-overview).</span></span>

- <span data-ttu-id="0035a-132">**Stockage Azure : les tables** sont un service Microsoft Azure qui permet aux développeurs de stocker des données structurées non SQL dans le Cloud, ce qui les rend facilement accessibles en tout lieu.</span><span class="sxs-lookup"><span data-stu-id="0035a-132">**Azure Storage: Tables** is a Microsoft Azure Service, which allows developers to store structured, non-SQL, data in the cloud, making it easily accessible anywhere.</span></span> <span data-ttu-id="0035a-133">Le service dispose d’une conception sans schéma, ce qui permet l’évolution des tables en fonction des besoins et est donc très flexible.</span><span class="sxs-lookup"><span data-stu-id="0035a-133">The Service boasts a schema-less design, allowing for the evolution of tables as needed, and thus is very flexible.</span></span> <span data-ttu-id="0035a-134">Pour plus d’informations, consultez la [page **tables Azure**](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span><span class="sxs-lookup"><span data-stu-id="0035a-134">For more information, visit the [**Azure Tables** page](https://docs.microsoft.com/azure/cosmos-db/table-storage-overview)</span></span>

<span data-ttu-id="0035a-135">Ce cours vous apprend à configurer et à utiliser le service IoT Hub, puis à visualiser une réponse fournie par un appareil.</span><span class="sxs-lookup"><span data-stu-id="0035a-135">This course will teach you how to setup and use the IoT Hub Service, and then visualize a response provided by a device.</span></span> <span data-ttu-id="0035a-136">Il vous faudra appliquer ces concepts à une configuration de service IoT Hub personnalisée, que vous pouvez générer.</span><span class="sxs-lookup"><span data-stu-id="0035a-136">It will be up to you to apply these concepts to a custom IoT Hub Service setup, which you might be building.</span></span>

## <a name="device-support"></a><span data-ttu-id="0035a-137">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="0035a-137">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="0035a-138">Course</span><span class="sxs-lookup"><span data-stu-id="0035a-138">Course</span></span></th><th style="width:150px"> <span data-ttu-id="0035a-139"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="0035a-139"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="0035a-140"><a href="immersive-headset-hardware-details.md">Casques immersifs</a></span><span class="sxs-lookup"><span data-stu-id="0035a-140"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="0035a-141">MR et Azure 313 : service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0035a-141">MR and Azure 313: IoT Hub Service</span></span></td><td style="text-align: center;"> <span data-ttu-id="0035a-142">✔️</span><span class="sxs-lookup"><span data-stu-id="0035a-142">✔️</span></span></td><td style="text-align: center;"> <span data-ttu-id="0035a-143">✔️</span><span class="sxs-lookup"><span data-stu-id="0035a-143">✔️</span></span></td>
</tr>
</table>

## <a name="prerequisites"></a><span data-ttu-id="0035a-144">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="0035a-144">Prerequisites</span></span>

<span data-ttu-id="0035a-145">Pour obtenir les conditions préalables les plus récentes concernant le développement avec la réalité mixte, y compris avec Microsoft HoloLens, consultez l’article [installer les outils](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) .</span><span class="sxs-lookup"><span data-stu-id="0035a-145">For the most up-to-date prerequisites for developing with mixed reality, including with the Microsoft HoloLens, visit the [Install the tools](https://docs.microsoft.com/windows/mixed-reality/install-the-tools) article.</span></span>

> [!NOTE]
> <span data-ttu-id="0035a-146">Ce didacticiel est conçu pour les développeurs qui ont une expérience de base avec Python.</span><span class="sxs-lookup"><span data-stu-id="0035a-146">This tutorial is designed for developers who have basic experience with Python.</span></span> <span data-ttu-id="0035a-147">Sachez également que les conditions préalables et les instructions écrites dans ce document représentent les éléments qui ont été testés et vérifiés au moment de la rédaction (juillet 2018).</span><span class="sxs-lookup"><span data-stu-id="0035a-147">Please also be aware that the prerequisites and written instructions within this document represent what has been tested and verified at the time of writing (July 2018).</span></span> <span data-ttu-id="0035a-148">Vous êtes libre d’utiliser le logiciel le plus récent, tel qu’indiqué dans l’article [installer les outils](install-the-tools.md) , bien qu’il ne soit pas supposé que les informations de ce cours correspondent parfaitement à ce que vous trouverez dans les logiciels plus récents que ceux répertoriés ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0035a-148">You are free to use the latest software, as listed within the [install the tools](install-the-tools.md) article, though it should not be assumed that the information in this course will perfectly match what you will find in newer software than that listed below.</span></span>

<span data-ttu-id="0035a-149">Le matériel et les logiciels suivants sont requis :</span><span class="sxs-lookup"><span data-stu-id="0035a-149">The following hardware and software is required:</span></span>

- <span data-ttu-id="0035a-150">Windows 10 automne Creators Update (ou version ultérieure), **mode développeur activé**</span><span class="sxs-lookup"><span data-stu-id="0035a-150">Windows 10 Fall Creators Update (or later), **Developer Mode enabled**</span></span>

    > [!WARNING]
    > <span data-ttu-id="0035a-151">Vous ne pouvez pas exécuter une machine virtuelle à l’aide d’Hyper-V sur Windows 10 édition personnelle.</span><span class="sxs-lookup"><span data-stu-id="0035a-151">You cannot run a Virtual Machine using Hyper-V on Windows 10 Home Edition.</span></span>

- <span data-ttu-id="0035a-152">SDK Windows 10 (dernière version)</span><span class="sxs-lookup"><span data-stu-id="0035a-152">Windows 10 SDK (latest version)</span></span>
- <span data-ttu-id="0035a-153">HoloLens, **mode développeur activé**</span><span class="sxs-lookup"><span data-stu-id="0035a-153">A HoloLens, **Developer Mode enabled**</span></span>
- <span data-ttu-id="0035a-154">Visual Studio 2017.15.4 (uniquement utilisé pour accéder à Azure Cloud Explorer)</span><span class="sxs-lookup"><span data-stu-id="0035a-154">Visual Studio 2017.15.4 (Only used to access the Azure Cloud Explorer)</span></span>
- <span data-ttu-id="0035a-155">Accès Internet pour Azure et pour IoT Hub service.</span><span class="sxs-lookup"><span data-stu-id="0035a-155">Internet Access for Azure, and for IoT Hub Service.</span></span> <span data-ttu-id="0035a-156">Pour plus d’informations, cliquez sur le lien ci-dessous [pour IOT Hub page de service](https://azure.microsoft.com/services/iot-hub/)</span><span class="sxs-lookup"><span data-stu-id="0035a-156">For more information, please follow this [link to IoT Hub Service page](https://azure.microsoft.com/services/iot-hub/)</span></span>
- <span data-ttu-id="0035a-157">Modèle de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="0035a-157">A machine learning model.</span></span> <span data-ttu-id="0035a-158">Si vous n’avez pas votre propre modèle prêt à l’emploi, [vous pouvez utiliser le modèle fourni avec ce cours](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).</span><span class="sxs-lookup"><span data-stu-id="0035a-158">If you do not have your own ready to use model, [you can use the model provided with this course](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip).</span></span>
- <span data-ttu-id="0035a-159">Logiciel **Hyper-V** activé sur votre ordinateur de développement Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0035a-159">**Hyper-V** software enabled on your Windows 10 development machine.</span></span>
- <span data-ttu-id="0035a-160">Une machine virtuelle exécutant Ubuntu (16,4 ou 18,4) en cours d’exécution sur votre ordinateur de développement. vous pouvez également utiliser un autre ordinateur exécutant Linux (Ubuntu 16,4 ou 18,4).</span><span class="sxs-lookup"><span data-stu-id="0035a-160">A Virtual Machine running Ubuntu (16.4 or 18.4), running on your development machine or alternatively you can use a separate computer running Linux (Ubuntu 16.4 or 18.4).</span></span> <span data-ttu-id="0035a-161">Vous trouverez plus d’informations sur la création d’une machine virtuelle sur Windows à l’aide d’Hyper-V dans le [chapitre « avant de commencer »](#before-you-start). (https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="0035a-161">You can find more information on how to create a VM on Windows using Hyper-V in the ["Before you Start" chapter](#before-you-start).(https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/quick-create-virtual-machine).</span></span>  



### <a name="before-you-start"></a><span data-ttu-id="0035a-162">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="0035a-162">Before you start</span></span>

1. <span data-ttu-id="0035a-163">Configurez et testez votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0035a-163">Set up and test your HoloLens.</span></span> <span data-ttu-id="0035a-164">Si vous avez besoin de la prise en charge de la configuration de votre HoloLens, [consultez l’article Configuration de hololens](https://docs.microsoft.com/hololens/hololens-setup).</span><span class="sxs-lookup"><span data-stu-id="0035a-164">If you need support setting up your HoloLens, [make sure to visit the HoloLens setup article](https://docs.microsoft.com/hololens/hololens-setup).</span></span>
2. <span data-ttu-id="0035a-165">Il est judicieux d’effectuer un réglage de l' **étalonnage** et du **capteur** au début du développement d’une nouvelle application HoloLens (parfois, il peut être utile d’effectuer ces tâches pour chaque utilisateur).</span><span class="sxs-lookup"><span data-stu-id="0035a-165">It is a good idea to perform **Calibration** and **Sensor Tuning** when beginning developing a new HoloLens app (sometimes it can help to perform those tasks for each user).</span></span>

<span data-ttu-id="0035a-166">Pour obtenir de l’aide sur l’étalonnage, veuillez suivre ce [lien vers l’article d’étalonnage HoloLens](calibration.md#hololens-2).</span><span class="sxs-lookup"><span data-stu-id="0035a-166">For help on Calibration, please follow this [link to the HoloLens Calibration article](calibration.md#hololens-2).</span></span>

<span data-ttu-id="0035a-167">Pour obtenir de l’aide sur le réglage du capteur, veuillez suivre ce [lien vers l’article sur le paramétrage du capteur HoloLens](sensor-tuning.md).</span><span class="sxs-lookup"><span data-stu-id="0035a-167">For help on Sensor Tuning, please follow this [link to the HoloLens Sensor Tuning article](sensor-tuning.md).</span></span>

3. <span data-ttu-id="0035a-168">Configurez votre **machine virtuelle Ubuntu** à l’aide d' **Hyper-V**.</span><span class="sxs-lookup"><span data-stu-id="0035a-168">Set up your **Ubuntu Virtual Machine** using **Hyper-V**.</span></span> <span data-ttu-id="0035a-169">Les ressources suivantes vous aideront à effectuer le processus.</span><span class="sxs-lookup"><span data-stu-id="0035a-169">The following resources will help you with the process.</span></span>
    1.  <span data-ttu-id="0035a-170">Tout d’abord, suivez ce lien pour [Télécharger le fichier ISO Ubuntu 16.04.4 LTS (Xenial Xerus)](https://au.releases.ubuntu.com/16.04/).</span><span class="sxs-lookup"><span data-stu-id="0035a-170">First, follow this link to [download the Ubuntu 16.04.4 LTS (Xenial Xerus) ISO](https://au.releases.ubuntu.com/16.04/).</span></span> <span data-ttu-id="0035a-171">Sélectionnez l' **image de bureau 64-bit PC (amd64)** .</span><span class="sxs-lookup"><span data-stu-id="0035a-171">Select the **64-bit PC (AMD64) desktop image**.</span></span>
    2.  <span data-ttu-id="0035a-172">Vérifiez que **Hyper-V** est activé sur votre ordinateur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0035a-172">Make sure **Hyper-V** is enabled on your Windows 10 machine.</span></span> <span data-ttu-id="0035a-173">Vous pouvez suivre ce lien pour obtenir des conseils sur [l’installation et l’activation d’Hyper-V sur Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span><span class="sxs-lookup"><span data-stu-id="0035a-173">You can follow this link for guidance on [installing and enabling Hyper-V on Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).</span></span>
    3.  <span data-ttu-id="0035a-174">Démarrez Hyper-V et créez une nouvelle machine virtuelle Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="0035a-174">Start Hyper-V and create a new Ubuntu VM.</span></span> <span data-ttu-id="0035a-175">Vous pouvez suivre ce lien pour obtenir un [Guide pas à pas sur la création d’une machine virtuelle avec Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine).</span><span class="sxs-lookup"><span data-stu-id="0035a-175">You can follow this link for a [step by step guide on how to create a VM with Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/create-virtual-machine).</span></span> <span data-ttu-id="0035a-176">Lorsque vous êtes invité à **« installer un système d’exploitation à partir d’un fichier image de démarrage »** , sélectionnez le fichier **ISO Ubuntu** que vous avez téléchargé plus tôt.</span><span class="sxs-lookup"><span data-stu-id="0035a-176">When requested to **"Install an operating system from a bootable image file"**, select the **Ubuntu ISO** you have download earlier.</span></span>

    > [!NOTE]
    > <span data-ttu-id="0035a-177">L’utilisation de la **création rapide Hyper-V** n’est pas suggérée.</span><span class="sxs-lookup"><span data-stu-id="0035a-177">Using **Hyper-V Quick Create** is not suggested.</span></span>  

## <a name="chapter-1---retrieve-the-custom-vision-model"></a><span data-ttu-id="0035a-178">Chapitre 1-récupération du modèle de Custom Vision</span><span class="sxs-lookup"><span data-stu-id="0035a-178">Chapter 1 - Retrieve the Custom Vision model</span></span>

<span data-ttu-id="0035a-179">Ce cours vous permet d’accéder à un [modèle de Custom vision prédéfini](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) qui détecte les claviers et les souris à partir d’images.</span><span class="sxs-lookup"><span data-stu-id="0035a-179">With this course you will have access to a [pre-built Custom Vision model](https://github.com/Microsoft/HolographicAcademy/raw/Azure-MixedReality-Labs/Azure%20Mixed%20Reality%20Labs/MR%20and%20Azure%20313%20-%20IoT%20Hub%20Service/Custom%20Vision%20Model.zip) that detects keyboards and mice from images.</span></span> <span data-ttu-id="0035a-180">Si vous utilisez cette valeur, passez au [Chapitre 2](#chapter-2---the-container-registry-service).</span><span class="sxs-lookup"><span data-stu-id="0035a-180">If you use this, proceed to [Chapter 2](#chapter-2---the-container-registry-service).</span></span>

<span data-ttu-id="0035a-181">Toutefois, vous pouvez suivre ces étapes si vous souhaitez utiliser votre propre Custom Vision modèle :</span><span class="sxs-lookup"><span data-stu-id="0035a-181">However, you can follow these steps if you wish to use your own Custom Vision model:</span></span>

1. <span data-ttu-id="0035a-182">Dans votre **projet Custom vision** , accédez à l’onglet **performances** .</span><span class="sxs-lookup"><span data-stu-id="0035a-182">In your **Custom Vision Project** go to the **Performance** tab.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0035a-183">Votre modèle doit utiliser un domaine *compact* pour exporter le modèle.</span><span class="sxs-lookup"><span data-stu-id="0035a-183">Your model must use a *compact* domain, to export the model.</span></span> <span data-ttu-id="0035a-184">Vous pouvez modifier votre domaine de modèles dans les paramètres de votre projet.</span><span class="sxs-lookup"><span data-stu-id="0035a-184">You can change your models domain in the settings for your project.</span></span>

    ![onglet performances](images/AzureLabs-Lab313-01.png)

2. <span data-ttu-id="0035a-186">Sélectionnez l' **itération** que vous souhaitez exporter, puis cliquez sur **Exporter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-186">Select the **Iteration** you want to export and click on **Export**.</span></span> <span data-ttu-id="0035a-187">Un panneau s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0035a-187">A blade will appear.</span></span>

    ![panneau exporter](images/AzureLabs-Lab313-02.png)

3. <span data-ttu-id="0035a-189">Dans le panneau, cliquez sur le fichier de l' **ancrage**.</span><span class="sxs-lookup"><span data-stu-id="0035a-189">In the blade click **Docker File**.</span></span>

    ![sélectionner un ancrage](images/AzureLabs-Lab313-03.png)

4. <span data-ttu-id="0035a-191">Dans le menu déroulant, cliquez sur **Linux** , puis sur **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="0035a-191">Click **Linux** in the drop-down menu and then click on **Download**.</span></span>

    ![Cliquez sur Télécharger](images/AzureLabs-Lab313-04.png)

5. <span data-ttu-id="0035a-193">Décompressez le contenu.</span><span class="sxs-lookup"><span data-stu-id="0035a-193">Unzip the content.</span></span> <span data-ttu-id="0035a-194">Vous l’utiliserez plus loin dans ce cours.</span><span class="sxs-lookup"><span data-stu-id="0035a-194">You will use it later in this course.</span></span>

## <a name="chapter-2---the-container-registry-service"></a><span data-ttu-id="0035a-195">Chapitre 2-service Container Registry</span><span class="sxs-lookup"><span data-stu-id="0035a-195">Chapter 2 - The Container Registry Service</span></span>

<span data-ttu-id="0035a-196">Le **Service Container Registry** est le référentiel utilisé pour héberger vos conteneurs.</span><span class="sxs-lookup"><span data-stu-id="0035a-196">The **Container Registry Service** is the repository used to host your containers.</span></span>

<span data-ttu-id="0035a-197">Le **service IOT Hub** que vous allez générer et utiliser dans ce cours fait référence à **Container Registry service** pour obtenir les conteneurs à déployer sur votre appareil Edge.</span><span class="sxs-lookup"><span data-stu-id="0035a-197">The **IoT Hub Service** that you will build and use in this course, refers to **Container Registry Service** to obtain the containers to deploy in your Edge Device.</span></span>

1. <span data-ttu-id="0035a-198">Tout d’abord, suivez ce [lien vers le portail Azure](https://portal.azure.com/)et connectez-vous avec vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0035a-198">First, follow this [link to the Azure Portal](https://portal.azure.com/), and login with your credentials.</span></span>

2. <span data-ttu-id="0035a-199">Accédez à **créer une ressource** et recherchez **Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="0035a-199">Go to **Create a resource** and look for **Container Registry**.</span></span>

    ![Registre de conteneurs](images/AzureLabs-Lab313-05.png)

3. <span data-ttu-id="0035a-201">Cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-201">Click on **Create**.</span></span>

    ![](images/AzureLabs-Lab313-06.png)

4. <span data-ttu-id="0035a-202">Définissez les paramètres de configuration du service :</span><span class="sxs-lookup"><span data-stu-id="0035a-202">Set the Service setup parameters:</span></span>

    1. <span data-ttu-id="0035a-203">Insérez un nom pour votre projet, dans cet exemple, son appelé **IoTCRegistry**.</span><span class="sxs-lookup"><span data-stu-id="0035a-203">Insert a name for your project, In this example its called **IoTCRegistry**.</span></span>

    2. <span data-ttu-id="0035a-204">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="0035a-204">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="0035a-205">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-205">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="0035a-206">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="0035a-206">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

    3. <span data-ttu-id="0035a-207">Définissez l’emplacement du service.</span><span class="sxs-lookup"><span data-stu-id="0035a-207">Set the location of the Service.</span></span>

    4. <span data-ttu-id="0035a-208">Définissez **utilisateur administrateur** sur **activer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-208">Set **Admin user** to **Enable**.</span></span>

    5. <span data-ttu-id="0035a-209">Définissez **SKU** sur de **base**.</span><span class="sxs-lookup"><span data-stu-id="0035a-209">Set **SKU** to **Basic**.</span></span> 

    ![](images/AzureLabs-Lab313-07.png)

5. <span data-ttu-id="0035a-210">Cliquez sur **créer** et attendez que les services soient créés.</span><span class="sxs-lookup"><span data-stu-id="0035a-210">Click **Create** and wait for the Services to be created.</span></span> 

6. <span data-ttu-id="0035a-211">Une fois que la notification s’affiche pour vous informer de la réussite de la création de l' *Container Registry*, cliquez sur **accéder à la ressource** pour être redirigé vers la page de votre service.</span><span class="sxs-lookup"><span data-stu-id="0035a-211">Once the notification pops up informing you of the successful creation of the *Container Registry*, click on **Go to resource** to be redirected to your Service page.</span></span>

    ![](images/AzureLabs-Lab313-08.png)

7. <span data-ttu-id="0035a-212">Dans la page service *Container Registry* , cliquez sur **clés d’accès**.</span><span class="sxs-lookup"><span data-stu-id="0035a-212">In the *Container Registry* Service page, click on **Access keys**.</span></span>

8. <span data-ttu-id="0035a-213">Prenez note (vous pouvez utiliser votre bloc-notes) des paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="0035a-213">Take note (you could use your Notepad) of the following parameters:</span></span>
    1. <span data-ttu-id="0035a-214">**Serveur de connexion**</span><span class="sxs-lookup"><span data-stu-id="0035a-214">**Login Server**</span></span>
    2. <span data-ttu-id="0035a-215">**Nom d’utilisateur**</span><span class="sxs-lookup"><span data-stu-id="0035a-215">**Username**</span></span>
    3. <span data-ttu-id="0035a-216">**Mot de passe**</span><span class="sxs-lookup"><span data-stu-id="0035a-216">**Password**</span></span>

    ![](images/AzureLabs-Lab313-09.png)

## <a name="chapter-3---the-iot-hub-service"></a><span data-ttu-id="0035a-217">Chapitre 3-service IoT Hub</span><span class="sxs-lookup"><span data-stu-id="0035a-217">Chapter 3 - The IoT Hub Service</span></span>

<span data-ttu-id="0035a-218">À présent, vous allez commencer la création et la configuration de votre **Service IOT Hub**.</span><span class="sxs-lookup"><span data-stu-id="0035a-218">Now you will begin the creation and setup of your **IoT Hub Service**.</span></span>

1. <span data-ttu-id="0035a-219">Si vous n’êtes pas déjà connecté, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0035a-219">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2.  <span data-ttu-id="0035a-220">Une fois connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche, recherchez **IOT Hub**, puis cliquez sur **entrée**.</span><span class="sxs-lookup"><span data-stu-id="0035a-220">Once logged in, click on **Create a resource** in the top left corner, and search for **IoT Hub**, and click **Enter**.</span></span>

 ![Rechercher le compte de stockage](images/AzureLabs-Lab313-10.png)

3.  <span data-ttu-id="0035a-222">La nouvelle page fournit une description du service de **compte de stockage** .</span><span class="sxs-lookup"><span data-stu-id="0035a-222">The new page will provide a description of the **Storage account** Service.</span></span> <span data-ttu-id="0035a-223">En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="0035a-223">At the bottom left of this prompt, click the **Create** button, to create an instance of this Service.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-11.png)

4.  <span data-ttu-id="0035a-225">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0035a-225">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="0035a-226">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="0035a-226">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="0035a-227">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-227">A resource group provides a way to monitor, control access, provision and manage billing for a collection of Azure assets.</span></span> <span data-ttu-id="0035a-228">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="0035a-228">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="0035a-229">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="0035a-229">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>


    2. <span data-ttu-id="0035a-230">Sélectionnez un **emplacement** approprié (utilisez le même emplacement pour tous les services que vous créez dans ce cours).</span><span class="sxs-lookup"><span data-stu-id="0035a-230">Select an appropriate **Location** (Use the same location across all the Services you create in this course).</span></span>

    3. <span data-ttu-id="0035a-231">Insérez le **nom** de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="0035a-231">Insert your desired **Name** for this Service instance.</span></span>    

5.  <span data-ttu-id="0035a-232">En bas de la page, cliquez sur **suivant : taille et échelle**.</span><span class="sxs-lookup"><span data-stu-id="0035a-232">On the bottom of the page click on **Next: Size and scale**.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-12.png)

6.  <span data-ttu-id="0035a-234">Dans cette page, sélectionnez votre **niveau de tarification et** de mise à l’échelle (s’il s’agit de votre première instance de service IOT Hub, vous devez disposer d’un niveau gratuit).</span><span class="sxs-lookup"><span data-stu-id="0035a-234">In this page, select your **Pricing and scale tier** (if this is your first IoT Hub Service instance, a free tier should be available to you).</span></span>  

7.  <span data-ttu-id="0035a-235">Cliquez sur **révision + créer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-235">Click on **Review + Create**.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-13.png)

8.  <span data-ttu-id="0035a-237">Passez en revue vos paramètres, puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-237">Review your settings and click on **Create**.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-14.png)

9. <span data-ttu-id="0035a-239">Une fois que la notification s’affiche pour vous informer de la réussite de la création du service *IOT Hub* , cliquez sur **accéder à la ressource** pour être redirigé vers votre page de service.</span><span class="sxs-lookup"><span data-stu-id="0035a-239">Once the notification pops up informing you of the successful creation of the *IoT Hub* Service, click on **Go to resource** to be redirected to your Service page.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-15.png)

10. <span data-ttu-id="0035a-241">Faites défiler le panneau latéral sur la gauche jusqu’à ce que la *gestion automatique des appareils*s’affiche, cliquez sur **IOT Edge**.</span><span class="sxs-lookup"><span data-stu-id="0035a-241">Scroll the side panel on the left until you see *Automatic Device Management*, the click on **IoT Edge**.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-16.png)

11. <span data-ttu-id="0035a-243">Dans la fenêtre qui s’affiche à droite, cliquez sur **ajouter IOT Edge appareil**.</span><span class="sxs-lookup"><span data-stu-id="0035a-243">In the window that appears to the right, click on **Add IoT Edge Device**.</span></span> <span data-ttu-id="0035a-244">Un panneau s’affiche à droite.</span><span class="sxs-lookup"><span data-stu-id="0035a-244">A blade will appear to the right.</span></span>

12. <span data-ttu-id="0035a-245">Dans le panneau, fournissez à votre nouvel appareil un **ID d’appareil** (le nom de votre choix).</span><span class="sxs-lookup"><span data-stu-id="0035a-245">In the blade, provide your new device a **Device ID** (a name of your choice).</span></span> <span data-ttu-id="0035a-246">Cliquez ensuite sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-246">Then, click **Save**.</span></span> <span data-ttu-id="0035a-247">Les clés *primaires* et *secondaires* seront générées automatiquement, si la **génération automatique** est cochée.</span><span class="sxs-lookup"><span data-stu-id="0035a-247">The *Primary* and *Secondary Keys* will auto generate, if you have **Auto Generate** ticked.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-17.png)

13. <span data-ttu-id="0035a-249">Vous revenez à la section *IOT Edge Devices* , où votre nouveau périphérique sera listé.</span><span class="sxs-lookup"><span data-stu-id="0035a-249">You will navigate back to the *IoT Edge Devices* section, where your new device will be listed.</span></span> <span data-ttu-id="0035a-250">Cliquez sur votre nouvel appareil (indiqué en rouge dans l’image ci-dessous).</span><span class="sxs-lookup"><span data-stu-id="0035a-250">Click on your new device (outlined in red in the below image).</span></span> 

    ![créer une instance de stockage](images/AzureLabs-Lab313-18.png)

14. <span data-ttu-id="0035a-252">Sur la page Détails de l' *appareil* qui s’affiche, effectuez une copie de la **chaîne de connexion** (clé primaire).</span><span class="sxs-lookup"><span data-stu-id="0035a-252">On the *Device Details* page that appears, take a copy of the **Connection String** (primary key).</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-19.png)

15. <span data-ttu-id="0035a-254">Revenez au volet de gauche, puis cliquez sur *stratégies d’accès partagé*pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="0035a-254">Go back to the panel on the left, and click *Shared access policies*, to open it.</span></span> 

16. <span data-ttu-id="0035a-255">Sur la page qui s’affiche, cliquez sur **iothubowner**. un panneau s’affiche à droite de l’écran.</span><span class="sxs-lookup"><span data-stu-id="0035a-255">On the page that appears, click **iothubowner**, and a blade will appear to the right of the screen.</span></span> 

17. <span data-ttu-id="0035a-256">Prenez note (dans votre bloc-notes) de la **chaîne de connexion** (clé primaire), pour une utilisation ultérieure lors de la définition de la *chaîne de connexion* à votre appareil.</span><span class="sxs-lookup"><span data-stu-id="0035a-256">Take note (on your Notepad) of the **Connection string** (primary key), for later use when setting the *Connection String* to your device.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-20.png)

## <a name="chapter-4---setting-up-the-development-environment"></a><span data-ttu-id="0035a-258">Chapitre 4-Configuration de l’environnement de développement</span><span class="sxs-lookup"><span data-stu-id="0035a-258">Chapter 4 - Setting up the development environment</span></span>

<span data-ttu-id="0035a-259">Pour créer et déployer des modules pour *IOT Hub Edge*, vous devez installer les composants suivants sur votre ordinateur de développement exécutant Windows 10 :</span><span class="sxs-lookup"><span data-stu-id="0035a-259">In order to create and deploy modules for *IoT Hub Edge*, you will require the following components installed on your development machine running Windows 10:</span></span>

1.  <span data-ttu-id="0035a-260">[Docker pour Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), vous êtes invité à créer un compte pour pouvoir effectuer le téléchargement.</span><span class="sxs-lookup"><span data-stu-id="0035a-260">[Docker for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows), it will ask you to create an account to be able to download.</span></span> 

    <span data-ttu-id="0035a-261">[![télécharger l’ancrage pour Windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)</span><span class="sxs-lookup"><span data-stu-id="0035a-261">[![download docker for windows](images/AzureLabs-Lab313-21.png)](https://store.docker.com/editions/community/docker-ce-desktop-windows)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="0035a-262">L’ancrage requiert *Windows 10 professionnel*, *Enterprise 14393*ou *Windows Server 2016 RTM*pour s’exécuter.</span><span class="sxs-lookup"><span data-stu-id="0035a-262">Docker requires *Windows 10 PRO*, *Enterprise 14393*, or *Windows Server 2016 RTM*, to run.</span></span> <span data-ttu-id="0035a-263">Si vous exécutez d’autres versions de Windows 10, vous pouvez essayer d’installer l’outil d’ancrage à l’aide de la [boîte à outils](https://docs.docker.com/toolbox/toolbox_install_windows/)de l’ancrage.</span><span class="sxs-lookup"><span data-stu-id="0035a-263">If you are running other versions of Windows 10, you can try installing Docker using the [Docker Toolbox](https://docs.docker.com/toolbox/toolbox_install_windows/).</span></span>

2.  <span data-ttu-id="0035a-264">[Python 3,6](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="0035a-264">[Python 3.6](https://www.python.org/downloads/).</span></span>

    <span data-ttu-id="0035a-265">[![Télécharger python 3,6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)</span><span class="sxs-lookup"><span data-stu-id="0035a-265">[![download python 3.6](images/AzureLabs-Lab313-22.png)](https://www.python.org/downloads/)</span></span>

3.  <span data-ttu-id="0035a-266">[Visual Studio code (également appelé vs code)](https://code.visualstudio.com/download).</span><span class="sxs-lookup"><span data-stu-id="0035a-266">[Visual Studio Code (also known as VS Code)](https://code.visualstudio.com/download).</span></span>

    <span data-ttu-id="0035a-267">[Télécharger ![VS Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="0035a-267">[![download VS Code](images/AzureLabs-Lab313-23.png)](https://code.visualstudio.com/download)</span></span>

<span data-ttu-id="0035a-268">Après avoir installé le logiciel mentionné ci-dessus, vous devrez redémarrer votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0035a-268">After installing the software mentioned above, you will need to restart your machine.</span></span>

## <a name="chapter-5---setting-up-the-ubuntu-environment"></a><span data-ttu-id="0035a-269">Chapitre 5-Configuration de l’environnement Ubuntu</span><span class="sxs-lookup"><span data-stu-id="0035a-269">Chapter 5 - Setting up the Ubuntu environment</span></span>

<span data-ttu-id="0035a-270">Vous pouvez maintenant passer à la configuration de votre appareil **exécutant le système d’exploitation Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="0035a-270">Now you can move on to setting up your device **running Ubuntu OS**.</span></span> <span data-ttu-id="0035a-271">Suivez les étapes ci-dessous pour installer les logiciels nécessaires, afin de déployer vos conteneurs sur votre tableau :</span><span class="sxs-lookup"><span data-stu-id="0035a-271">Follow the steps below, to install the necessary software, to deploy your containers on your board:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0035a-272">Vous devez toujours précéder les commandes de terminal avec **sudo** pour qu’elles s’exécutent en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="0035a-272">You should always precede the terminal commands with **sudo** to run as admin user.</span></span> <span data-ttu-id="0035a-273">celles</span><span class="sxs-lookup"><span data-stu-id="0035a-273">i.e:</span></span>
> 
>   ```bash
>   sudo docker \<option> \<command> \<argument>
>   ```

1.  <span data-ttu-id="0035a-274">Ouvrez le **Terminal Ubuntu**et utilisez la commande suivante pour installer **PIP**:</span><span class="sxs-lookup"><span data-stu-id="0035a-274">Open the **Ubuntu Terminal**, and use the following command to install **pip**:</span></span>

    > [! Conseil]<span data-ttu-id="0035a-275"> vous pouvez ouvrir le *Terminal* très facilement à l’aide du raccourci clavier : **CTRL + ALT + T**.</span><span class="sxs-lookup"><span data-stu-id="0035a-275"> You can open *Terminal* very easily through using the keyboard shortcut: **Ctrl + Alt + T**.</span></span>

    ```bash
        sudo apt-get install python-pip
    ```

2.  <span data-ttu-id="0035a-276">Tout au long de ce chapitre, vous pouvez être invité, par *Terminal*, à utiliser le stockage de votre appareil. pour entrer **y/n** (oui ou non), tapez **« y »** , puis appuyez sur la touche **entrée** pour accepter.</span><span class="sxs-lookup"><span data-stu-id="0035a-276">Throughout this Chapter, you may be prompted, by *Terminal*, for permission to use your device storage, and for you to input **y/n** (yes or no), type **'y'**, and then press the **Enter** key, to accept.</span></span>

3.  <span data-ttu-id="0035a-277">Une fois cette commande terminée, utilisez la commande suivante pour installer la **boucle**:</span><span class="sxs-lookup"><span data-stu-id="0035a-277">Once that command has completed, use the following command to install **curl**:</span></span>

    ```bash
        sudo apt install curl
    ```

4.  <span data-ttu-id="0035a-278">Une fois **PIP** et **bouclé** installés, utilisez la commande suivante pour installer le **Runtime IOT Edge**, ce qui est nécessaire pour déployer et contrôler les modules de votre tableau :</span><span class="sxs-lookup"><span data-stu-id="0035a-278">Once **pip** and **curl** are installed, use the following command to install the **IoT Edge runtime**, this is necessary to deploy and control the modules on your board:</span></span>

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

5. <span data-ttu-id="0035a-279">À ce stade, vous serez invité à ouvrir le fichier de *configuration du runtime*, à insérer la **chaîne de connexion**de l’appareil, que vous avez noté (dans votre bloc-notes), lors de la création du **service IOT Hub** ([à l’étape 14, du chapitre 3](#chapter-3---the-iot-hub-service)).</span><span class="sxs-lookup"><span data-stu-id="0035a-279">At this point you will be prompted to open up the *runtime config file*, to insert the **Device Connection String**, that you noted down (in your Notepad), when creating the **IoT Hub Service** ([at step 14, of Chapter 3](#chapter-3---the-iot-hub-service)).</span></span> <span data-ttu-id="0035a-280">Exécutez la ligne suivante sur le terminal pour ouvrir ce fichier :</span><span class="sxs-lookup"><span data-stu-id="0035a-280">Run the following line on the terminal to open that file:</span></span>

    ```bash
        sudo nano /etc/iotedge/config.yaml
    ```

6. <span data-ttu-id="0035a-281">Le fichier **config. YAML** s’affiche et vous pouvez le modifier :</span><span class="sxs-lookup"><span data-stu-id="0035a-281">The **config.yaml** file will be displayed, ready for you to edit:</span></span>

    > [!WARNING]
    > <span data-ttu-id="0035a-282">Lorsque ce fichier s’ouvre, il peut être quelque peu déroutant.</span><span class="sxs-lookup"><span data-stu-id="0035a-282">When this file opens, it may be somewhat confusing.</span></span> <span data-ttu-id="0035a-283">Vous allez modifier le texte de ce fichier, au sein du *Terminal* lui-même.</span><span class="sxs-lookup"><span data-stu-id="0035a-283">You will be text editing this file, within the *Terminal* itself.</span></span> 

    1.  <span data-ttu-id="0035a-284">Utilisez les touches de direction de votre clavier pour faire défiler vers le bas (vous devez faire défiler une petite façon) pour atteindre la ligne contenant « :</span><span class="sxs-lookup"><span data-stu-id="0035a-284">Use the arrow keys on your keyboard to scroll down (you will need to scroll down a little way), to reach the line containing":</span></span>

        <span data-ttu-id="0035a-285">« **\<ajouter la chaîne de connexion de l’appareil ici >** ».</span><span class="sxs-lookup"><span data-stu-id="0035a-285">"**\<ADD DEVICE CONNECTION STRING HERE>**".</span></span>

    2. <span data-ttu-id="0035a-286">Ligne de remplacement, **y compris les crochets**, avec la **chaîne de connexion** de l’appareil que vous avez notée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0035a-286">Substitute line, **including the brackets**, with the **Device Connection String** you have noted earlier.</span></span>

7. <span data-ttu-id="0035a-287">Une fois votre chaîne de connexion en place, sur votre clavier, appuyez sur les touches **CTRL-X** pour enregistrer le fichier.</span><span class="sxs-lookup"><span data-stu-id="0035a-287">With your Connection String in place, on your keyboard, press the **Ctrl-X** keys to save the file.</span></span> <span data-ttu-id="0035a-288">Vous êtes invité à confirmer en tapant **Y**. Appuyez ensuite sur la touche **entrée** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="0035a-288">It will ask you to confirm by typing **Y**. Then, press the **Enter** key, to confirm.</span></span> <span data-ttu-id="0035a-289">Vous allez revenir au *Terminal*standard.</span><span class="sxs-lookup"><span data-stu-id="0035a-289">You will go back to the regular *Terminal*.</span></span> 

8. <span data-ttu-id="0035a-290">Une fois que l’exécution de ces commandes est terminée, vous avez installé le **Runtime IOT Edge**.</span><span class="sxs-lookup"><span data-stu-id="0035a-290">Once these commands have all run successfully, you will have installed the **IoT Edge Runtime**.</span></span> <span data-ttu-id="0035a-291">Une fois initialisé, le runtime démarre automatiquement chaque fois que l’appareil est mis sous tension, et se assiste en arrière-plan, en attendant que les modules soient déployés à partir du **Service IOT Hub**.</span><span class="sxs-lookup"><span data-stu-id="0035a-291">Once initialized, the runtime will start on its own every time the device is powered up, and will sit in the background, waiting for modules to be deployed from the **IoT Hub Service**.</span></span>

9.  <span data-ttu-id="0035a-292">Exécutez la ligne de commande suivante pour initialiser le *Runtime IOT Edge*:</span><span class="sxs-lookup"><span data-stu-id="0035a-292">Run the following command line to initialize the *IoT Edge Runtime*:</span></span>

    ```bash
        sudo systemctl restart iotedge
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="0035a-293">Si vous apportez des modifications à votre fichier. YAML, ou au programme d’installation ci-dessus, vous devrez réexécuter la ligne de redémarrage ci-dessus, dans le *Terminal*.</span><span class="sxs-lookup"><span data-stu-id="0035a-293">If you make changes to your .yaml file, or the above setup, you will need to run the above restart line again, within *Terminal*.</span></span>

10. <span data-ttu-id="0035a-294">Vérifiez l’état de l' *exécution de IOT Edge* en exécutant la ligne de commande suivante.</span><span class="sxs-lookup"><span data-stu-id="0035a-294">Check the *IoT Edge Runtime* status by running the following command line.</span></span> <span data-ttu-id="0035a-295">Le Runtime doit s’afficher avec l’état **actif (en cours d’exécution)** en texte vert.</span><span class="sxs-lookup"><span data-stu-id="0035a-295">The runtime should appear with the status **active (running)** in green text.</span></span>

    ```bash
        sudo systemctl status iotedge
    ```

11. <span data-ttu-id="0035a-296">Appuyez sur les touches **Ctrl + C** pour quitter la page d’État.</span><span class="sxs-lookup"><span data-stu-id="0035a-296">Press the **Ctrl-C** keys, to exit the status page.</span></span> <span data-ttu-id="0035a-297">Vous pouvez vérifier que le *Runtime IOT Edge* récupère correctement les conteneurs en tapant la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-297">You can verify that the *IoT Edge Runtime* is pulling the containers correctly by typing the following command:</span></span>

    ```bash
        sudo docker ps
    ```

12. <span data-ttu-id="0035a-298">Une liste contenant deux (2) conteneurs doit s’afficher.</span><span class="sxs-lookup"><span data-stu-id="0035a-298">A list with two (2) containers should appear.</span></span> <span data-ttu-id="0035a-299">Il s’agit des modules par défaut qui sont créés automatiquement par le service IoT Hub (edgeAgent et edgeHub).</span><span class="sxs-lookup"><span data-stu-id="0035a-299">These are the default modules that are automatically created by the IoT Hub Service (edgeAgent and edgeHub).</span></span> <span data-ttu-id="0035a-300">Une fois que vous avez créé et déployé vos propres modules, ceux-ci s’affichent dans cette liste, sous les paramètres par défaut.</span><span class="sxs-lookup"><span data-stu-id="0035a-300">Once you create and deploy your own modules, they will appear in this list, underneath the default ones.</span></span>

## <a name="chapter-6---install-the-extensions"></a><span data-ttu-id="0035a-301">Chapitre 6-installer les extensions</span><span class="sxs-lookup"><span data-stu-id="0035a-301">Chapter 6 - Install the extensions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0035a-302">Les chapitres suivants (6-9) doivent être exécutés sur votre ordinateur Windows 10.</span><span class="sxs-lookup"><span data-stu-id="0035a-302">The next few Chapters (6-9) are to be performed on your Windows 10 machine.</span></span>

1. <span data-ttu-id="0035a-303">Ouvrez **vs code**.</span><span class="sxs-lookup"><span data-stu-id="0035a-303">Open **VS Code**.</span></span>

2. <span data-ttu-id="0035a-304">Cliquez sur le bouton **Extensions** (carré) dans la barre de gauche de vs code pour ouvrir le **panneau extensions**.</span><span class="sxs-lookup"><span data-stu-id="0035a-304">Click on the **Extensions** (square) button on the left bar of VS Code, to open the **Extensions panel**.</span></span>

3. <span data-ttu-id="0035a-305">Recherchez et installez les extensions suivantes (comme indiqué dans l’image ci-dessous) :</span><span class="sxs-lookup"><span data-stu-id="0035a-305">Search for, and install, the following extensions (as shown in the image below):</span></span>

    1. <span data-ttu-id="0035a-306">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="0035a-306">Azure IoT Edge</span></span>
    2. <span data-ttu-id="0035a-307">Boîte à outils Azure IoT</span><span class="sxs-lookup"><span data-stu-id="0035a-307">Azure IoT Toolkit</span></span>
    3. <span data-ttu-id="0035a-308">Docker</span><span class="sxs-lookup"><span data-stu-id="0035a-308">Docker</span></span>   

    ![Créer votre conteneur](images/AzureLabs-Lab313-24.png)

4. <span data-ttu-id="0035a-310">Une fois les extensions installées, fermez et rouvrez VS Code.</span><span class="sxs-lookup"><span data-stu-id="0035a-310">Once the extensions are installed, close and re-open VS Code.</span></span>

5. <span data-ttu-id="0035a-311">Une fois que VS Code ouvert, accédez à **affichage** > **Terminal intégré**.</span><span class="sxs-lookup"><span data-stu-id="0035a-311">With VS Code open once more, navigate to **View** > **Integrated terminal**.</span></span>

6. <span data-ttu-id="0035a-312">Vous allez maintenant installer **Cookiecutter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-312">You will now install **Cookiecutter**.</span></span> <span data-ttu-id="0035a-313">Dans le terminal, exécutez la commande bash suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-313">In the terminal run the following bash command:</span></span>

    ```bash
        pip install --upgrade --user cookiecutter
    ```

    > [! Conseil]<span data-ttu-id="0035a-314"> Si vous rencontrez des problèmes avec cette commande :</span><span class="sxs-lookup"><span data-stu-id="0035a-314"> If you have trouble with this command:</span></span> 
    >1. <span data-ttu-id="0035a-315">Redémarrez VS Code et/ou votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0035a-315">Restart VS Code, and/ or your computer.</span></span>
    >2. <span data-ttu-id="0035a-316">Il peut être nécessaire de basculer le **Terminal vs code** vers celui que vous avez utilisé pour installer Python, C.-à-d. **PowerShell** (en particulier si l’environnement python était déjà installé sur votre ordinateur).</span><span class="sxs-lookup"><span data-stu-id="0035a-316">It might be necessary to switch the **VS Code Terminal** to the one you have been using to install Python, i.e. **Powershell** (especially in case the Python environment was already installed on your machine).</span></span> <span data-ttu-id="0035a-317">Une fois le terminal ouvert, vous trouverez le menu déroulant sur le côté droit du terminal.</span><span class="sxs-lookup"><span data-stu-id="0035a-317">With the Terminal open, you will find the drop down menu on the right side of the Terminal.</span></span>
     <span data-ttu-id="0035a-318">![créer votre conteneur](images/AzureLabs-Lab313-24b.png)</span><span class="sxs-lookup"><span data-stu-id="0035a-318">![Create your container](images/AzureLabs-Lab313-24b.png)</span></span> 
    >3. <span data-ttu-id="0035a-319">Assurez-vous que le chemin d’installation de **python** est ajouté en tant que **variable d’environnement** sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0035a-319">Make sure the **Python** installation path is added as **Environment Variable** on your machine.</span></span> <span data-ttu-id="0035a-320">Cookiecutter doit faire partie du même chemin d’emplacement.</span><span class="sxs-lookup"><span data-stu-id="0035a-320">Cookiecutter should be part of the same location path.</span></span> <span data-ttu-id="0035a-321">[Pour plus d’informations sur les variables d’environnement](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx), cliquez sur le lien suivant :</span><span class="sxs-lookup"><span data-stu-id="0035a-321">Please follow this [link for more information on Environment Variables](https://msdn.microsoft.com/library/windows/desktop/ms682653(v=vs.85).aspx),</span></span> 

7. <span data-ttu-id="0035a-322">Une fois l’installation de **Cookiecutter** terminée, vous devez redémarrer votre ordinateur pour que **Cookiecutter** soit reconnu en tant que commande dans l’environnement de votre système.</span><span class="sxs-lookup"><span data-stu-id="0035a-322">Once **Cookiecutter** has finished installing, you should restart your machine, so that **Cookiecutter** is recognized as a command, within your System's environment.</span></span>

## <a name="chapter-7---create-your-container-solution"></a><span data-ttu-id="0035a-323">Chapitre 7-créer votre solution de conteneur</span><span class="sxs-lookup"><span data-stu-id="0035a-323">Chapter 7 - Create your container solution</span></span>

<span data-ttu-id="0035a-324">À ce stade, vous devez créer le conteneur, avec le module, pour faire l’objet d’un push dans le *Container Registry*.</span><span class="sxs-lookup"><span data-stu-id="0035a-324">At this point, you need to create the container, with the module, to be pushed into the *Container Registry*.</span></span> <span data-ttu-id="0035a-325">Une fois que vous avez poussé votre conteneur, vous allez utiliser le service *IOT Hub Edge* pour le déployer sur votre appareil, qui exécute le *IOT Edge Runtime*.</span><span class="sxs-lookup"><span data-stu-id="0035a-325">Once you have pushed your container, you will use the *IoT Hub Edge* Service to deploy it to your device, which is running the *IoT Edge runtime*.</span></span>

1. <span data-ttu-id="0035a-326">Dans VS Code, cliquez sur **afficher** > **palette de commandes**.</span><span class="sxs-lookup"><span data-stu-id="0035a-326">From VS Code, click **View** > **Command palette**.</span></span>

2. <span data-ttu-id="0035a-327">Dans la palette, recherchez et exécutez **Azure IOT Edge : nouvelle solution IOT Edge**.</span><span class="sxs-lookup"><span data-stu-id="0035a-327">In the palette, search and run **Azure IoT Edge: New Iot Edge Solution**.</span></span>

3. <span data-ttu-id="0035a-328">Accédez à l’emplacement où vous souhaitez créer votre solution.</span><span class="sxs-lookup"><span data-stu-id="0035a-328">Browse into a location where you want to create your solution.</span></span> <span data-ttu-id="0035a-329">Appuyez sur la touche **entrée** pour accepter l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="0035a-329">Press the **Enter** key, to accept the location.</span></span>

4. <span data-ttu-id="0035a-330">Donnez un nom à votre solution.</span><span class="sxs-lookup"><span data-stu-id="0035a-330">Give a name to your solution.</span></span> <span data-ttu-id="0035a-331">Appuyez sur la touche **entrée** pour confirmer le nom fourni.</span><span class="sxs-lookup"><span data-stu-id="0035a-331">Press the **Enter** key, to confirm your provided name.</span></span>

5. <span data-ttu-id="0035a-332">Vous êtes maintenant invité à choisir l’infrastructure de modèle pour votre solution.</span><span class="sxs-lookup"><span data-stu-id="0035a-332">Now you will be prompted to choose the template framework for your solution.</span></span> <span data-ttu-id="0035a-333">Cliquez sur **module python**.</span><span class="sxs-lookup"><span data-stu-id="0035a-333">Click **Python Module**.</span></span> <span data-ttu-id="0035a-334">Appuyez sur la touche **entrée** pour confirmer ce choix.</span><span class="sxs-lookup"><span data-stu-id="0035a-334">Press the **Enter** key, to confirm this choice.</span></span>

6. <span data-ttu-id="0035a-335">Donnez un nom à votre module.</span><span class="sxs-lookup"><span data-stu-id="0035a-335">Give a name to your module.</span></span> <span data-ttu-id="0035a-336">Appuyez sur la touche **entrée** pour confirmer le nom de votre module.</span><span class="sxs-lookup"><span data-stu-id="0035a-336">Press the **Enter** key, to confirm the name of your module.</span></span> <span data-ttu-id="0035a-337">Veillez à prendre note (avec votre bloc-notes) du nom du module, car il est utilisé ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="0035a-337">Make sure to take a note (with your Notepad) of the module name, as it is used later.</span></span>

7. <span data-ttu-id="0035a-338">Vous remarquerez que l’adresse d’un *référentiel d’images d’ancrage* prédéfini s’affichera dans la palette.</span><span class="sxs-lookup"><span data-stu-id="0035a-338">You will notice a pre-built *Docker Image Repository* address will appear on the palette.</span></span> <span data-ttu-id="0035a-339">Elle doit ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="0035a-339">It will look like:</span></span>

    <span data-ttu-id="0035a-340">**localhost : 5000/-le nom de votre module-** .</span><span class="sxs-lookup"><span data-stu-id="0035a-340">**localhost:5000/-THE NAME OF YOUR MODULE-**.</span></span> 

8. <span data-ttu-id="0035a-341">Supprimez **localhost : 5000**et, à sa place, insérez l’adresse du **serveur de connexion** *Container Registry* , que vous avez notée lors de la création du **service Container Registry** ([à l’étape 8, du chapitre 2](#chapter-2---the-container-registry-service)).</span><span class="sxs-lookup"><span data-stu-id="0035a-341">Delete **localhost:5000**, and in its place insert the *Container Registry* **Login Server** address, which you noted when creating the **Container Registry Service** ([in step 8, of Chapter 2](#chapter-2---the-container-registry-service)).</span></span> <span data-ttu-id="0035a-342">Appuyez sur la touche **entrée** pour confirmer l’adresse.</span><span class="sxs-lookup"><span data-stu-id="0035a-342">Press the **Enter** key, to confirm the address.</span></span>

9. <span data-ttu-id="0035a-343">À ce stade, la solution contenant le modèle pour votre module Python est créée et sa structure s’affiche sous l' **onglet Explorer**, de vs code, sur le côté gauche de l’écran.</span><span class="sxs-lookup"><span data-stu-id="0035a-343">At this point, the solution containing the template for your Python module will be created and its structure will be displayed in the **Explore Tab**, of VS Code, on the left side of the screen.</span></span> <span data-ttu-id="0035a-344">Si l' **onglet Explorer** n’est pas ouvert, vous pouvez l’ouvrir en cliquant sur le bouton supérieur, dans la barre à gauche.</span><span class="sxs-lookup"><span data-stu-id="0035a-344">If the **Explore Tab** is not open, you can open it by clicking the top-most button, in the bar on the left.</span></span>

    ![Créer votre conteneur](images/AzureLabs-Lab313-25.png)

10. <span data-ttu-id="0035a-346">La dernière étape de ce chapitre consiste à cliquer et à ouvrir le **fichier. env**, à partir de l' **onglet Explorer**, et à ajouter votre **nom d’utilisateur** et votre **mot de passe** *Container Registry* .</span><span class="sxs-lookup"><span data-stu-id="0035a-346">The last step for this Chapter, is to click and open the **.env file**, from within the **Explore Tab**, and add your *Container Registry* **username** and **password**.</span></span> <span data-ttu-id="0035a-347">Ce fichier est ignoré par git, mais lors de la création du conteneur, les informations d’identification sont définies pour accéder au **Service Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="0035a-347">This file is ignored by git, but on building the container, will set the credentials to access the **Container Registry Service**.</span></span>

    ![Créer votre conteneur](images/AzureLabs-Lab313-26.png)

## <a name="chapter-8---editing-your-container-solution"></a><span data-ttu-id="0035a-349">Chapitre 8-modification de votre solution de conteneur</span><span class="sxs-lookup"><span data-stu-id="0035a-349">Chapter 8 - Editing your container solution</span></span>

<span data-ttu-id="0035a-350">Vous allez maintenant terminer la solution Container, en mettant à jour les fichiers suivants :</span><span class="sxs-lookup"><span data-stu-id="0035a-350">You will now complete the container solution, by updating the following files:</span></span>

- <span data-ttu-id="0035a-351">*main<span></span>. py* python script.</span><span class="sxs-lookup"><span data-stu-id="0035a-351">*main<span></span>.py* python script.</span></span>
- <span data-ttu-id="0035a-352">*Requirements. txt*.</span><span class="sxs-lookup"><span data-stu-id="0035a-352">*requirements.txt*.</span></span>
- <span data-ttu-id="0035a-353">*Deployment. template. JSON*.</span><span class="sxs-lookup"><span data-stu-id="0035a-353">*deployment.template.json*.</span></span>
- <span data-ttu-id="0035a-354">*Fichier dockerfile. amd64*</span><span class="sxs-lookup"><span data-stu-id="0035a-354">*Dockerfile.amd64*</span></span>

<span data-ttu-id="0035a-355">Vous allez ensuite créer le dossier *images* , utilisé par le script Python pour rechercher les images à faire correspondre à votre *modèle de Custom vision*.</span><span class="sxs-lookup"><span data-stu-id="0035a-355">You will then create the *images* folder, used by the python script to check for images to match against your *Custom Vision model*.</span></span> <span data-ttu-id="0035a-356">Enfin, vous allez ajouter le fichier *labels. txt* , pour vous aider à lire votre modèle et le fichier *Model. PB* , qui est votre modèle.</span><span class="sxs-lookup"><span data-stu-id="0035a-356">Lastly, you will add the *labels.txt* file, to help read your model, and the *model.pb* file, which is your model.</span></span>

1. <span data-ttu-id="0035a-357">Avec VS Code ouvrir, accédez à votre dossier de module, puis recherchez le script nommé **main<span></span>. py**.</span><span class="sxs-lookup"><span data-stu-id="0035a-357">With VS Code open, navigate to your module folder, and look for the script called **main<span></span>.py**.</span></span> <span data-ttu-id="0035a-358">Double-cliquez pour l’ouvrir.</span><span class="sxs-lookup"><span data-stu-id="0035a-358">Double-click to open it.</span></span>

2. <span data-ttu-id="0035a-359">Supprimez le contenu du fichier et insérez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="0035a-359">Delete the content of the file and insert the following code:</span></span>

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

3.  <span data-ttu-id="0035a-360">Ouvrez le fichier nommé **Requirements. txt**et remplacez son contenu par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0035a-360">Open the file called **requirements.txt**, and substitute its content with the following:</span></span>

    ```
    azure-iothub-device-client==1.4.0.0b3
    opencv-python==3.3.1.11
    tensorflow==1.8.0
    pillow==5.1.0
    ```

4.  <span data-ttu-id="0035a-361">Ouvrez le fichier nommé **Deployment. template. JSON**et remplacez son contenu en suivant les instructions ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0035a-361">Open the file called **deployment.template.json**, and substitute its content following the below guideline:</span></span>

    1. <span data-ttu-id="0035a-362">Étant donné que vous aurez votre propre structure JSON unique, vous devrez la modifier manuellement (plutôt que de copier un exemple).</span><span class="sxs-lookup"><span data-stu-id="0035a-362">Because you will have your own, unique, JSON structure, you will need to edit it by hand (rather than copying an example).</span></span> <span data-ttu-id="0035a-363">Pour faciliter cette opération, utilisez l’image ci-dessous comme guide.</span><span class="sxs-lookup"><span data-stu-id="0035a-363">To make this easy, use the below image as a guide.</span></span>
    2. <span data-ttu-id="0035a-364">Les zones qui sont différentes des vôtres, mais que vous ne **devez pas modifier sont mises en surbrillance en jaune**.</span><span class="sxs-lookup"><span data-stu-id="0035a-364">Areas which will look different to yours, but which you **should NOT change are highlighted yellow**.</span></span>
    3. <span data-ttu-id="0035a-365">**Les sections que vous devez supprimer sont en rouge.**</span><span class="sxs-lookup"><span data-stu-id="0035a-365">**Sections which you need to delete, are a highlighted red.**</span></span>
    4. <span data-ttu-id="0035a-366">Veillez à supprimer les crochets appropriés et à supprimer également les virgules.</span><span class="sxs-lookup"><span data-stu-id="0035a-366">Be careful to delete the correct brackets, and also remove the commas.</span></span>

        ![Créer votre conteneur](images/AzureLabs-Lab313-27.png)

    5. <span data-ttu-id="0035a-368">Le JSON complet doit ressembler à l’image suivante (avec les différences uniques suivantes : *nom d’utilisateur/mot de passe/nom de module/références de module*) :</span><span class="sxs-lookup"><span data-stu-id="0035a-368">The completed JSON should look like the following image (though, with your unique differences: *username/password/module name/module references*):</span></span>

        ![Créer votre conteneur](images/AzureLabs-Lab313-28.png)

5.  <span data-ttu-id="0035a-370">Ouvrez le fichier nommé **fichier dockerfile. amd64**et remplacez son contenu par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0035a-370">Open the file called **Dockerfile.amd64**, and substitute its content with the following:</span></span>

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

6.  <span data-ttu-id="0035a-371">Cliquez avec le bouton droit sur le dossier sous **modules** (il porte le nom que vous avez fourni précédemment. dans cet exemple, il est appelé *pythonmodule*), puis cliquez sur **nouveau dossier**.</span><span class="sxs-lookup"><span data-stu-id="0035a-371">Right-click on the folder beneath **modules** (it will have the name you provided previously; in the example further down, it is called *pythonmodule*), and click on **New Folder**.</span></span> <span data-ttu-id="0035a-372">Nommez le dossier **images**.</span><span class="sxs-lookup"><span data-stu-id="0035a-372">Name the folder **images**.</span></span>

7.  <span data-ttu-id="0035a-373">Dans le dossier, ajoutez des images contenant la souris ou le clavier.</span><span class="sxs-lookup"><span data-stu-id="0035a-373">Inside the folder, add some images containing mouse or keyboard.</span></span> <span data-ttu-id="0035a-374">Il s’agira des images qui seront analysées par le modèle Tensorflow.</span><span class="sxs-lookup"><span data-stu-id="0035a-374">Those will be the images that will be analyzed by the Tensorflow model.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0035a-375">Si vous utilisez votre propre modèle, vous devrez le modifier pour refléter vos propres données de modèles.</span><span class="sxs-lookup"><span data-stu-id="0035a-375">If you are using your own model, you will need to change this to reflect your own models data.</span></span>

8.  <span data-ttu-id="0035a-376">Vous devez maintenant récupérer les fichiers **labels. txt** et **Model. PB** à partir du dossier Model, que vous avez précédemment téléchargé (ou créé à partir de votre propre **service vision personnalisée**), au [Chapitre 1](#chapter-1---retrieve-the-custom-vision-model).</span><span class="sxs-lookup"><span data-stu-id="0035a-376">You will now need to retrieve the **labels.txt** and **model.pb** files from the model folder, which you previous downloaded (or created from your own **Custom Vision Service**), in [Chapter 1](#chapter-1---retrieve-the-custom-vision-model).</span></span> <span data-ttu-id="0035a-377">Une fois que vous avez les fichiers, placez-les dans votre solution, en même temps que les autres fichiers.</span><span class="sxs-lookup"><span data-stu-id="0035a-377">Once you have the files, place them within your solution, alongside the other files.</span></span> <span data-ttu-id="0035a-378">Le résultat final doit ressembler à l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0035a-378">The final result should look like the image below:</span></span>

    ![Créer votre conteneur](images/AzureLabs-Lab313-29.png)

## <a name="chapter-9---package-the-solution-as-a-container"></a><span data-ttu-id="0035a-380">Chapitre 9-empaqueter la solution en tant que conteneur</span><span class="sxs-lookup"><span data-stu-id="0035a-380">Chapter 9 - Package the solution as a container</span></span>

1.  <span data-ttu-id="0035a-381">Vous êtes maintenant prêt à « empaqueter » vos fichiers en tant que conteneur et à les envoyer à votre **Azure Container Registry**.</span><span class="sxs-lookup"><span data-stu-id="0035a-381">You are now ready to "package" your files as a container and push it to your **Azure Container Registry**.</span></span> <span data-ttu-id="0035a-382">Dans VS Code, ouvrez le *Terminal intégré* (**Affichez** > **terminal intégré** ou **CTRL**+ **\`** ), puis utilisez la ligne suivante pour vous connecter à **dockr** (remplacez les valeurs de la commande par les informations d’identification de votre **Azure Container Registry (ACR)** ) :</span><span class="sxs-lookup"><span data-stu-id="0035a-382">Within VS Code, open the *Integrated Terminal* (**View** > **Integrated Terminal** or **Ctrl**+**\`**), and use the following line to login to **Docker** (substitute the values of the command with the credentials of your **Azure Container Registry (ACR)**):</span></span>

    ```bash
        docker login -u <ACR username> -p <ACR password> <ACR login server>
    ```

2. <span data-ttu-id="0035a-383">Cliquez avec le bouton droit sur le fichier **Deployment. template. JSON**, puis cliquez sur **générer IOT Edge solution**.</span><span class="sxs-lookup"><span data-stu-id="0035a-383">Right-click on the file **deployment.template.json**, and click **Build IoT Edge Solution**.</span></span> <span data-ttu-id="0035a-384">Ce processus de génération prend un certain temps (en fonction de votre appareil), soyez donc prêt à attendre.</span><span class="sxs-lookup"><span data-stu-id="0035a-384">This build process takes quite some time (depending on your device), so be prepared to wait.</span></span> <span data-ttu-id="0035a-385">Une fois le processus de génération terminé, un fichier de **déploiement. JSON** a été créé dans un nouveau dossier nommé **config**.</span><span class="sxs-lookup"><span data-stu-id="0035a-385">After the build process finishes, a **deployment.json** file will have been created inside a new folder called **config**.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-30.png)

3. <span data-ttu-id="0035a-387">Rouvrez la **palette de commandes** et recherchez **Azure : se connecter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-387">Open the **Command Palette** again, and search for **Azure: Sign In**.</span></span> <span data-ttu-id="0035a-388">Suivez les invites à l’aide des informations d’identification de votre compte Azure. VS Code vous fournira une option de *copie et d’ouverture*, qui copiera le code de l’appareil dont vous aurez bientôt besoin et ouvrira votre navigateur Web par défaut.</span><span class="sxs-lookup"><span data-stu-id="0035a-388">Follow the prompts using your Azure Account credentials; VS Code will provide you with an option to *Copy and Open*, which will copy the device code you will soon need, and open your default web browser.</span></span> <span data-ttu-id="0035a-389">Lorsque vous y êtes invité, collez le code de l’appareil pour authentifier votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0035a-389">When asked, paste the device code, to authenticate your machine.</span></span>

    ![copier et ouvrir](images/AzureLabs-Lab313-31.png)

4. <span data-ttu-id="0035a-391">Une fois que vous êtes connecté, vous remarquerez, sur le côté inférieur du panneau d' *exploration* , une nouvelle section appelée **appareils Azure IOT Hub**.</span><span class="sxs-lookup"><span data-stu-id="0035a-391">Once signed in you will notice, on the bottom side of the *Explore* panel, a new section called **Azure IoT Hub Devices**.</span></span> <span data-ttu-id="0035a-392">Cliquez sur cette section pour la développer.</span><span class="sxs-lookup"><span data-stu-id="0035a-392">Click this section to expand it.</span></span>

    ![appareil de périphérie](images/AzureLabs-Lab313-32.png)

5. <span data-ttu-id="0035a-394">Si votre appareil n’est pas ici, vous devez cliquer avec le bouton droit sur *Azure IOT Hub Devices*, puis cliquer sur **définir IOT Hub chaîne de connexion**.</span><span class="sxs-lookup"><span data-stu-id="0035a-394">If your device is not here, you will need to right-click *Azure IoT Hub Devices*, and then click **Set IoT Hub Connection String**.</span></span> <span data-ttu-id="0035a-395">Vous verrez alors que la **palette de commandes** (en haut de vs code) vous invitera à entrer votre *chaîne de connexion*.</span><span class="sxs-lookup"><span data-stu-id="0035a-395">You will then see that the **Command Palette** (at the top of VS Code), will prompt you to input your *Connection String*.</span></span> <span data-ttu-id="0035a-396">Il s’agit de la *chaîne de connexion* que vous avez notée à la fin du [chapitre 3](#chapter-3---the-iot-hub-service).</span><span class="sxs-lookup"><span data-stu-id="0035a-396">This is the *Connection String* you noted down at the end of [Chapter 3](#chapter-3---the-iot-hub-service).</span></span> <span data-ttu-id="0035a-397">Appuyez sur la touche **entrée** , une fois que vous avez copié la chaîne dans.</span><span class="sxs-lookup"><span data-stu-id="0035a-397">Press the **Enter** key, once you have copied the string in.</span></span>    

6. <span data-ttu-id="0035a-398">Votre appareil doit se charger et s’afficher.</span><span class="sxs-lookup"><span data-stu-id="0035a-398">Your device should load, and appear.</span></span> <span data-ttu-id="0035a-399">Cliquez avec le bouton droit sur le nom de l’appareil, puis cliquez sur **créer un déploiement pour un seul appareil**.</span><span class="sxs-lookup"><span data-stu-id="0035a-399">Right-click on the device name, and then click, **Create Deployment for Single Device**.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-33b.png)

7. <span data-ttu-id="0035a-401">Une invite de l' *Explorateur de fichiers* s’affiche, dans laquelle vous pouvez accéder au dossier **config** , puis sélectionner le fichier **Deployment. JSON** .</span><span class="sxs-lookup"><span data-stu-id="0035a-401">You will get a *File Explorer* prompt, where you can navigate to the **config** folder, and then select the **deployment.json** file.</span></span> <span data-ttu-id="0035a-402">Une fois ce fichier sélectionné, cliquez sur le bouton **Sélectionner le manifeste de déploiement Edge** .</span><span class="sxs-lookup"><span data-stu-id="0035a-402">With that file selected, click the **Select Edge Deployment Manifest** button.</span></span>

    ![créer un déploiement](images/AzureLabs-Lab313-34.png)

8. <span data-ttu-id="0035a-404">À ce stade, vous avez fourni à votre **Service IOT Hub** le manifeste pour le déploiement de votre conteneur, en tant que module, à partir de votre **Azure Container Registry**, en le déployant efficacement sur votre appareil.</span><span class="sxs-lookup"><span data-stu-id="0035a-404">At this point you have provided your **IoT Hub Service** with the manifest for it to deploy your container, as a module, from your **Azure Container Registry**, effectively deploying it to your device.</span></span>

9. <span data-ttu-id="0035a-405">Pour afficher les messages envoyés à partir de votre appareil au IoT Hub, cliquez à nouveau avec le bouton droit sur le nom de votre appareil dans la section **appareils IOT Hub Azure** , dans le panneau **Explorateur** , puis cliquez sur **Démarrer l’analyse du message D2C**.</span><span class="sxs-lookup"><span data-stu-id="0035a-405">To view the messages sent from your device to the IoT Hub, right-click again on your device name in the **Azure IoT Hub Devices** section, in the **Explorer** panel, and click on **Start Monitoring D2C Message**.</span></span> <span data-ttu-id="0035a-406">Les messages envoyés à partir de votre appareil doivent apparaître dans le terminal VS.</span><span class="sxs-lookup"><span data-stu-id="0035a-406">The messages sent from your device should appear in the VS Terminal.</span></span> <span data-ttu-id="0035a-407">Soyez patient, car cela peut prendre un certain temps.</span><span class="sxs-lookup"><span data-stu-id="0035a-407">Be patient, as this may take some time.</span></span> <span data-ttu-id="0035a-408">Consultez le chapitre suivant pour le débogage et vérification de la réussite du déploiement.</span><span class="sxs-lookup"><span data-stu-id="0035a-408">See the next Chapter for debugging, and checking if deployment was successful.</span></span>

<span data-ttu-id="0035a-409">Ce module va à présent itérer entre les images du dossier **images** et les analyser, avec chaque itération.</span><span class="sxs-lookup"><span data-stu-id="0035a-409">This module will now iterate between the images in the **images** folder and analyze them, with each iteration.</span></span> <span data-ttu-id="0035a-410">Il s’agit évidemment d’une démonstration de la façon d’obtenir le modèle de Machine Learning de base pour travailler dans un environnement d’appareil IoT Edge.</span><span class="sxs-lookup"><span data-stu-id="0035a-410">This is obviously just a demonstration of how to get the basic machine learning model to work in an IoT Edge device environment.</span></span> 

<span data-ttu-id="0035a-411">Pour développer les fonctionnalités de cet exemple, vous pouvez procéder de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="0035a-411">To expand the functionality of this example, you could proceed in several ways.</span></span> <span data-ttu-id="0035a-412">L’une des façons peut inclure du code dans le conteneur, qui capture les photos à partir d’une webcam connectée à l’appareil et enregistre les images dans le dossier images.</span><span class="sxs-lookup"><span data-stu-id="0035a-412">One way could be including some code in the container, that captures photos from a webcam that is connected to the device, and saves the images in the images folder.</span></span> 

<span data-ttu-id="0035a-413">Vous pouvez également copier les images à partir de l’appareil IoT dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="0035a-413">Another way could be copying the images from the IoT device into the container.</span></span> <span data-ttu-id="0035a-414">Pour ce faire, il est pratique d’exécuter la commande suivante dans le terminal de l’appareil IoT (peut-être une petite application peut-elle effectuer le travail, si vous souhaitez automatiser le processus).</span><span class="sxs-lookup"><span data-stu-id="0035a-414">A practical way to do that is to run the following command in the IoT device Terminal (perhaps a small app could do the job, if you wished to automate the process).</span></span> <span data-ttu-id="0035a-415">Vous pouvez tester cette commande en l’exécutant manuellement à partir de l’emplacement du dossier où sont stockés vos fichiers :</span><span class="sxs-lookup"><span data-stu-id="0035a-415">You can test this command by running it manually from the folder location where your files are stored:</span></span>

```bash
    sudo docker cp <filename> <modulename>:/app/images/<a name of your choice>
```

## <a name="chapter-10---debugging-the-iot-edge-runtime"></a><span data-ttu-id="0035a-416">Chapitre 10-débogage du runtime IoT Edge</span><span class="sxs-lookup"><span data-stu-id="0035a-416">Chapter 10 - Debugging the IoT Edge Runtime</span></span>

<span data-ttu-id="0035a-417">Vous trouverez ci-dessous une liste de lignes de commande et de conseils pour vous aider à surveiller et à déboguer l’activité de messagerie du *IOT Edge Runtime*, à partir de votre **appareil Ubuntu**.</span><span class="sxs-lookup"><span data-stu-id="0035a-417">The following are a list of command lines, and tips, to help you monitor and debug the messaging activity of the *IoT Edge Runtime*, from your **Ubuntu device**.</span></span> 

- <span data-ttu-id="0035a-418">Vérifiez l’état de l' *exécution de IOT Edge* en exécutant la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-418">Check the *IoT Edge Runtime* status by running the following command line:</span></span>

    ```bash
        sudo systemctl status iotedge
    ```

    > [!NOTE]
    > <span data-ttu-id="0035a-419">N’oubliez pas d’appuyer sur **Ctrl + C**pour terminer l’affichage de l’État.</span><span class="sxs-lookup"><span data-stu-id="0035a-419">Remember to press **Ctrl + C**, to finish viewing the status.</span></span>

- <span data-ttu-id="0035a-420">Répertorie les conteneurs qui sont actuellement déployés.</span><span class="sxs-lookup"><span data-stu-id="0035a-420">List the containers that are currently deployed.</span></span> <span data-ttu-id="0035a-421">Si le *Service IOT Hub* a déployé correctement les conteneurs, ceux-ci sont affichés en exécutant la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-421">If the *IoT Hub Service* has deployed the containers successfully, they will be displayed by running the following command line:</span></span>

    ```bash
        sudo iotedge list
    ```

    <span data-ttu-id="0035a-422">Ou</span><span class="sxs-lookup"><span data-stu-id="0035a-422">Or</span></span>

    ```bash
        sudo docker ps
    ```

    > [!NOTE]
    > <span data-ttu-id="0035a-423">L’exemple ci-dessus est un bon moyen de vérifier si votre module a été correctement déployé, tel qu’il apparaîtra dans la liste. Sinon, vous ne verrez **que** *edgeHub* et *edgeAgent*.</span><span class="sxs-lookup"><span data-stu-id="0035a-423">The above is a good way to check whether your module has been deployed successfully, as it will appear in the list; you will otherwise **only** see the *edgeHub* and *edgeAgent*.</span></span>

- <span data-ttu-id="0035a-424">Pour afficher les journaux de code d’un conteneur, exécutez la ligne de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-424">To display the code logs of a container, run the following command line:</span></span>

    ```bash
        journalctl -u iotedge
    ```

<span data-ttu-id="0035a-425">**Commandes utiles pour gérer le runtime IoT Edge :**</span><span class="sxs-lookup"><span data-stu-id="0035a-425">**Useful commands to manage the IoT Edge Runtime:**</span></span>

-  <span data-ttu-id="0035a-426">Pour supprimer tous les conteneurs de l’hôte :</span><span class="sxs-lookup"><span data-stu-id="0035a-426">To delete all containers in the host:</span></span>

    ```bash
        sudo docker rm -f $(sudo docker ps -aq)
    ```

-  <span data-ttu-id="0035a-427">Pour arrêter l' *exécution du IOT Edge*:</span><span class="sxs-lookup"><span data-stu-id="0035a-427">To stop the *IoT Edge Runtime*:</span></span>

    ```bash
        sudo systemctl stop iotedge
    ```

## <a name="chapter-11---create-table-service"></a><span data-ttu-id="0035a-428">Chapitre 11-créer un service de table</span><span class="sxs-lookup"><span data-stu-id="0035a-428">Chapter 11 - Create Table Service</span></span> 

<span data-ttu-id="0035a-429">Revenez à votre portail Azure, où vous allez créer un service de tables Azure, en créant une ressource de stockage.</span><span class="sxs-lookup"><span data-stu-id="0035a-429">Navigate back to your Azure Portal, where you will create an Azure Tables Service, by creating a Storage resource.</span></span>

1. <span data-ttu-id="0035a-430">Si vous n’êtes pas déjà connecté, connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0035a-430">If not already signed in, log into the [Azure Portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="0035a-431">Une fois connecté, cliquez sur **créer une ressource**, dans le coin supérieur gauche, recherchez compte de **stockage**, puis appuyez sur la touche **entrée** pour lancer la recherche.</span><span class="sxs-lookup"><span data-stu-id="0035a-431">Once logged in, click on **Create a resource**, in the top left corner, and search for **Storage account**, and press the **Enter** key, to start the search.</span></span>

3. <span data-ttu-id="0035a-432">Une fois qu’il s’est affiché, cliquez sur **compte de stockage-BLOB, fichier, table, file d’attente** dans la liste.</span><span class="sxs-lookup"><span data-stu-id="0035a-432">Once it has appeared, click **Storage account - blob, file, table, queue** from the list.</span></span>

    ![Rechercher le compte de stockage](images/AzureLabs-Lab313-35.png)

4. <span data-ttu-id="0035a-434">La nouvelle page fournit une description du service de **compte de stockage** .</span><span class="sxs-lookup"><span data-stu-id="0035a-434">The new page will provide a description of the **Storage account** Service.</span></span> <span data-ttu-id="0035a-435">En bas à gauche de cette invite, cliquez sur le bouton **créer** pour créer une instance de ce service.</span><span class="sxs-lookup"><span data-stu-id="0035a-435">At the bottom left of this prompt, click the **Create** button, to create an instance of this Service.</span></span>

    ![créer une instance de stockage](images/AzureLabs-Lab313-36.png)

5. <span data-ttu-id="0035a-437">Une fois que vous avez cliqué sur **créer**, un panneau s’affiche :</span><span class="sxs-lookup"><span data-stu-id="0035a-437">Once you have clicked on **Create**, a panel will appear:</span></span>

    1. <span data-ttu-id="0035a-438">Insérez le **nom** souhaité pour cette instance de service (*doit être tout en minuscules*).</span><span class="sxs-lookup"><span data-stu-id="0035a-438">Insert your desired **Name** for this Service instance (*must be all lowercase*).</span></span>

    2. <span data-ttu-id="0035a-439">Pour **modèle de déploiement**, cliquez sur **Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="0035a-439">For **Deployment model**, click **Resource manager**.</span></span>

    3. <span data-ttu-id="0035a-440">Pour **type de compte**, dans le menu déroulant, cliquez sur **stockage (v1 à usage général)** .</span><span class="sxs-lookup"><span data-stu-id="0035a-440">For **Account kind**, using the dropdown menu, click **Storage (general purpose v1)**.</span></span>

    4. <span data-ttu-id="0035a-441">Cliquez sur un **emplacement**approprié.</span><span class="sxs-lookup"><span data-stu-id="0035a-441">Click an appropriate **Location**.</span></span>
    
    5. <span data-ttu-id="0035a-442">Dans le menu déroulant **réplication** , cliquez sur **stockage avec accès géo-redondant (RA-GRS)** .</span><span class="sxs-lookup"><span data-stu-id="0035a-442">For the **Replication** dropdown menu, click **Read-access-geo-redundant storage (RA-GRS)**.</span></span>

    6. <span data-ttu-id="0035a-443">Pour les **performances**, cliquez sur **standard**.</span><span class="sxs-lookup"><span data-stu-id="0035a-443">For **Performance**, click **Standard**.</span></span>

    7. <span data-ttu-id="0035a-444">Dans la section **transfert sécurisé requis** , cliquez sur **désactivé**.</span><span class="sxs-lookup"><span data-stu-id="0035a-444">Within the **Secure transfer required** section, click **Disabled**.</span></span>

    8. <span data-ttu-id="0035a-445">Dans le menu déroulant **abonnement** , cliquez sur un abonnement approprié.</span><span class="sxs-lookup"><span data-stu-id="0035a-445">From the **Subscription** dropdown menu, click an appropriate subscription.</span></span>

    9. <span data-ttu-id="0035a-446">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="0035a-446">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="0035a-447">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-447">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="0035a-448">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="0035a-448">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="0035a-449">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="0035a-449">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    10. <span data-ttu-id="0035a-450">Laissez les **réseaux virtuels** **désactivés**, s’il s’agit d’une option pour vous.</span><span class="sxs-lookup"><span data-stu-id="0035a-450">Leave **Virtual networks** as **Disabled**, if this is an option for you.</span></span>

    11. <span data-ttu-id="0035a-451">Cliquez sur **Create (Créer)** .</span><span class="sxs-lookup"><span data-stu-id="0035a-451">Click **Create**.</span></span>

        ![renseigner les détails du stockage](images/AzureLabs-Lab313-37.png)

6. <span data-ttu-id="0035a-453">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="0035a-453">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

7. <span data-ttu-id="0035a-454">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="0035a-454">A notification will appear in the Portal once the Service instance is created.</span></span> <span data-ttu-id="0035a-455">Cliquez sur les notifications pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="0035a-455">Click on the notifications to explore your new Service instance.</span></span>

    ![nouvelle notification de stockage](images/AzureLabs-Lab313-38.png)

8. <span data-ttu-id="0035a-457">Cliquez sur le bouton **atteindre la ressource** dans la notification pour accéder à la page vue d’ensemble de votre nouvelle instance de service de stockage.</span><span class="sxs-lookup"><span data-stu-id="0035a-457">Click the **Go to resource** button in the notification, and you will be taken to your new Storage Service instance overview page.</span></span>

    ![accéder à la ressource](images/AzureLabs-Lab313-39.png)

9. <span data-ttu-id="0035a-459">Dans la page vue d’ensemble, sur le côté droit, cliquez sur **tables**.</span><span class="sxs-lookup"><span data-stu-id="0035a-459">From the overview page, to the right-hand side, click **Tables**.</span></span>
    
    ![elles](images/AzureLabs-Lab313-40.png)

10. <span data-ttu-id="0035a-461">Le panneau à droite change pour afficher les informations sur le **service de table** , où vous devez ajouter une nouvelle table.</span><span class="sxs-lookup"><span data-stu-id="0035a-461">The panel on the right will change to show the **Table Service** information, wherein you need to add a new table.</span></span> <span data-ttu-id="0035a-462">Pour ce faire, cliquez sur le bouton **+ table** dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="0035a-462">Do this by clicking the **+ Table** button to the top-left corner.</span></span>

    ![Tables ouvertes](images/AzureLabs-Lab313-41.png)

11. <span data-ttu-id="0035a-464">Une nouvelle page s’affiche, dans laquelle vous devez entrer un nom de **table**.</span><span class="sxs-lookup"><span data-stu-id="0035a-464">A new page will be shown, wherein you need to enter a **Table name**.</span></span> <span data-ttu-id="0035a-465">Il s’agit du nom que vous allez utiliser pour faire référence aux données de votre application dans les chapitres ultérieurs (création d’Function App et Power BI).</span><span class="sxs-lookup"><span data-stu-id="0035a-465">This is the name you will use to refer to the data in your application in later Chapters (creating Function App, and Power BI).</span></span> <span data-ttu-id="0035a-466">Insérez **IoTMessages** comme nom (vous pouvez choisir les vôtres, mémorisez-les quand vous les utilisez plus loin dans ce document), puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0035a-466">Insert **IoTMessages** as the name (you can choose your own, just remember it when used later in this document) and click **OK**.</span></span> 

12. <span data-ttu-id="0035a-467">Une fois la nouvelle table créée, vous pouvez la voir dans la page **service de table** (en bas).</span><span class="sxs-lookup"><span data-stu-id="0035a-467">Once the new table has been created, you will be able to see it within the **Table Service** page (at the bottom).</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-42.png)  

13. <span data-ttu-id="0035a-469">Maintenant, cliquez sur **clés d’accès** et copiez le **nom** et la **clé** du compte de stockage (à l’aide de votre bloc-notes). vous utiliserez ces valeurs plus loin dans ce cours, lors de la création de l' **Function App Azure**.</span><span class="sxs-lookup"><span data-stu-id="0035a-469">Now click on **Access keys** and take a copy of the **Storage account name** and **Key** (using your Notepad), you will use these values later in this course, when creating the **Azure Function App**.</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-43.png) 

14. <span data-ttu-id="0035a-471">À nouveau, à l’aide du panneau situé à gauche, faites défiler jusqu’à la section *service de table* , puis cliquez sur **tables** (ou **Parcourir les tables**, dans nouveaux portails) et prenez une copie de l’URL de la **table** (à l’aide de votre bloc-notes).</span><span class="sxs-lookup"><span data-stu-id="0035a-471">Using the panel on the left again, scroll to the *Table Service* section, and click **Tables** (or **Browse Tables**, in newer Portals) and take a copy of the **Table URL** (using your Notepad).</span></span> <span data-ttu-id="0035a-472">Vous utiliserez cette valeur plus loin dans ce cours, lors de la liaison de votre table à votre application **Power bi** .</span><span class="sxs-lookup"><span data-stu-id="0035a-472">You will use this value later in this course, when linking your table to your **Power BI** application.</span></span>

    ![nouvelle table créée](images/AzureLabs-Lab313-44.png)

## <a name="chapter-12---completing-the-azure-table"></a><span data-ttu-id="0035a-474">Chapitre 12-remplissage de la table Azure</span><span class="sxs-lookup"><span data-stu-id="0035a-474">Chapter 12 - Completing the Azure Table</span></span>

<span data-ttu-id="0035a-475">Maintenant que votre compte de stockage de **service de table** a été configuré, il est temps d’y ajouter des données qui seront utilisées pour stocker et récupérer des informations.</span><span class="sxs-lookup"><span data-stu-id="0035a-475">Now that your **Table Service** storage account has been setup, it is time to add data to it, which will be used to store and retrieve information.</span></span> <span data-ttu-id="0035a-476">La modification de vos tables peut être effectuée par le biais de **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="0035a-476">The editing of your Tables can be done through **Visual Studio**.</span></span>

1. <span data-ttu-id="0035a-477">Ouvrez **Visual Studio** (**pas** Visual Studio code).</span><span class="sxs-lookup"><span data-stu-id="0035a-477">Open **Visual Studio** (**not** Visual Studio Code).</span></span>

2. <span data-ttu-id="0035a-478">Dans le menu, cliquez sur **afficher** > **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-478">From the menu, click **View** > **Cloud Explorer**.</span></span>

    ![ouvrir Cloud Explorer](images/AzureLabs-Lab313-45.png)

3. <span data-ttu-id="0035a-480">Le **Cloud Explorer** s’ouvre en tant qu’élément ancré (patienter, car le chargement peut prendre du temps).</span><span class="sxs-lookup"><span data-stu-id="0035a-480">The **Cloud Explorer** will open as a docked item (be patient, as loading may take time).</span></span>

    > [!WARNING] 
    > <span data-ttu-id="0035a-481">Si l’abonnement que vous avez utilisé pour créer vos *comptes de stockage* n’est pas visible, vérifiez que vous disposez des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0035a-481">If the subscription you used to create your *Storage Accounts* is not visible, ensure that you have:</span></span> 
    > - <span data-ttu-id="0035a-482">Connectez-vous au même compte que celui que vous avez utilisé pour le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-482">Logged in to the same account as the one you used for the Azure Portal.</span></span>
    > - <span data-ttu-id="0035a-483">Sélectionnez votre abonnement dans la page de gestion des comptes (vous devrez peut-être appliquer un filtre à partir de vos paramètres de compte) :</span><span class="sxs-lookup"><span data-stu-id="0035a-483">Selected your subscription from the Account Management page (you may need to apply a filter from your account settings):</span></span>  
    >
    >   ![Rechercher un abonnement](images/AzureLabs-Lab313-46.png)

4. <span data-ttu-id="0035a-485">Vos services Cloud Azure s’affichent.</span><span class="sxs-lookup"><span data-stu-id="0035a-485">Your Azure cloud Services will be shown.</span></span> <span data-ttu-id="0035a-486">Recherchez les **comptes de stockage** et cliquez sur la flèche à gauche de celle-ci pour développer vos comptes.</span><span class="sxs-lookup"><span data-stu-id="0035a-486">Find **Storage Accounts** and click the arrow to the left of that to expand your accounts.</span></span>

    ![ouvrir les comptes de stockage](images/AzureLabs-Lab313-47.png)

5. <span data-ttu-id="0035a-488">Une fois développé, le **compte de stockage** que vous venez de créer doit être disponible.</span><span class="sxs-lookup"><span data-stu-id="0035a-488">Once expanded, your newly created **Storage account** should be available.</span></span> <span data-ttu-id="0035a-489">Cliquez sur la flèche à gauche de votre stockage, puis une fois celle-ci développée, recherchez des **tables** , puis cliquez sur la flèche en regard de celle-ci pour afficher la **table** que vous avez créée dans le dernier chapitre.</span><span class="sxs-lookup"><span data-stu-id="0035a-489">Click the arrow to the left of your storage, and then once that is expanded, find **Tables** and click the arrow next to that, to reveal the **Table** you created in the last Chapter.</span></span> <span data-ttu-id="0035a-490">Double-cliquez sur votre **table**.</span><span class="sxs-lookup"><span data-stu-id="0035a-490">Double-click your **Table**.</span></span>

6. <span data-ttu-id="0035a-491">Votre table s’ouvre au centre de votre fenêtre Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0035a-491">Your table will be opened in the center of your Visual Studio window.</span></span> <span data-ttu-id="0035a-492">Cliquez sur l’icône de table avec le **+** (plus).</span><span class="sxs-lookup"><span data-stu-id="0035a-492">Click the table icon with the **+** (plus) on it.</span></span>

    ![Ajouter une nouvelle table](images/AzureLabs-Lab313-48.png)

7. <span data-ttu-id="0035a-494">Une fenêtre s’affiche pour vous inviter à *Ajouter une entité*.</span><span class="sxs-lookup"><span data-stu-id="0035a-494">A window will appear prompting for you to *Add Entity*.</span></span> <span data-ttu-id="0035a-495">Vous ne créerez qu’une seule entité, bien qu’elle ait trois propriétés.</span><span class="sxs-lookup"><span data-stu-id="0035a-495">You will create only one entity, though it will have three properties.</span></span> <span data-ttu-id="0035a-496">Vous remarquerez que *PartitionKey* et *RowKey* sont déjà fournis, car ils sont utilisés par la table pour rechercher vos données.</span><span class="sxs-lookup"><span data-stu-id="0035a-496">You will notice that *PartitionKey* and *RowKey* are already provided, as these are used by the table to find your data.</span></span> 

    ![clé de partition et de ligne](images/AzureLabs-Lab313-49.png)

8. <span data-ttu-id="0035a-498">Mettez à jour les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="0035a-498">Update the following values:</span></span>

    - <span data-ttu-id="0035a-499">Nom : **PartitionKey**, valeur : **PK_IoTMessages**</span><span class="sxs-lookup"><span data-stu-id="0035a-499">Name: **PartitionKey**, Value: **PK_IoTMessages**</span></span> 

    - <span data-ttu-id="0035a-500">Nom : **RowKey**, valeur : **RK_1_IoTMessages**</span><span class="sxs-lookup"><span data-stu-id="0035a-500">Name: **RowKey**, Value: **RK_1_IoTMessages**</span></span> 

9. <span data-ttu-id="0035a-501">Ensuite, cliquez sur **Ajouter une propriété** (dans l’angle inférieur gauche de la fenêtre Ajouter une *entité* ) et ajoutez la propriété suivante :</span><span class="sxs-lookup"><span data-stu-id="0035a-501">Then, click **Add property** (to the lower left of the *Add Entity* window) and add the following property:</span></span>

    - <span data-ttu-id="0035a-502">**MessageContent**, en tant que *chaîne*, laissez la valeur vide.</span><span class="sxs-lookup"><span data-stu-id="0035a-502">**MessageContent**, as a *string*, leave the Value empty.</span></span>

10. <span data-ttu-id="0035a-503">Votre table doit correspondre à celle de l’image ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="0035a-503">Your table should match the one in the image below:</span></span>

    ![Ajouter les valeurs correctes](images/AzureLabs-Lab313-50.png)

    > [!NOTE] 
    > <span data-ttu-id="0035a-505">La raison pour laquelle l’entité a le numéro 1 dans la clé de ligne est que vous souhaiterez peut-être ajouter d’autres messages, si vous souhaitez approfondir ce cours.</span><span class="sxs-lookup"><span data-stu-id="0035a-505">The reason why the entity has the number 1 in the row key, is because you might want to add more messages, should you desire to experiment further with this course.</span></span>

11. <span data-ttu-id="0035a-506">Cliquez sur **OK** lorsque vous avez terminé.</span><span class="sxs-lookup"><span data-stu-id="0035a-506">Click **OK** when you are finished.</span></span> <span data-ttu-id="0035a-507">Votre table est maintenant prête à être utilisée.</span><span class="sxs-lookup"><span data-stu-id="0035a-507">Your table is now ready to be used.</span></span>

## <a name="chapter-13---create-an-azure-function-app"></a><span data-ttu-id="0035a-508">Chapitre 13-créer un Function App Azure</span><span class="sxs-lookup"><span data-stu-id="0035a-508">Chapter 13 - Create an Azure Function App</span></span> 

<span data-ttu-id="0035a-509">Il est maintenant temps de créer un *Function App Azure*, qui sera appelé par le *service IOT Hub* pour stocker les messages de l’appareil *IOT Edge* dans le service de **table** , que vous avez créé dans le chapitre précédent.</span><span class="sxs-lookup"><span data-stu-id="0035a-509">It is now time to create an *Azure Function App*, which will be called by the *IoT Hub Service* to store the *IoT Edge* device messages in the **Table** Service, which you created in the previous Chapter.</span></span>

<span data-ttu-id="0035a-510">Tout d’abord, vous devez créer un fichier qui permettra à votre fonction Azure de charger les bibliothèques dont vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="0035a-510">First, you need to create a file that will allow your Azure Function to load the libraries you need.</span></span>

1.  <span data-ttu-id="0035a-511">Ouvrez le **bloc-notes** (appuyez sur la *touche Windows*, puis tapez *Notepad*).</span><span class="sxs-lookup"><span data-stu-id="0035a-511">Open **Notepad** (press the *Windows Key*, and type *notepad*).</span></span>

    ![ouvrir le bloc-notes](images/AzureLabs-Lab313-51.png)

2.  <span data-ttu-id="0035a-513">Avec le bloc-notes ouvert, insérez la structure JSON ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0035a-513">With Notepad open, insert the JSON structure below into it.</span></span> <span data-ttu-id="0035a-514">Une fois que vous avez effectué cette opération, enregistrez-la sur votre bureau en tant que **Project. JSON**.</span><span class="sxs-lookup"><span data-stu-id="0035a-514">Once you have done that, save it on your desktop as **project.json**.</span></span> <span data-ttu-id="0035a-515">Ce fichier définit les bibliothèques que votre fonction utilisera.</span><span class="sxs-lookup"><span data-stu-id="0035a-515">This file defines the libraries your function will use.</span></span> <span data-ttu-id="0035a-516">Si vous avez utilisé NuGet, il vous semblera familier.</span><span class="sxs-lookup"><span data-stu-id="0035a-516">If you have used NuGet, it will look familiar.</span></span>
    
    > [!WARNING]
    > <span data-ttu-id="0035a-517">Il est important que le nom soit correct ; Assurez-vous qu’il n' **a pas d’extension de fichier. txt** .</span><span class="sxs-lookup"><span data-stu-id="0035a-517">It is important that the naming is correct; ensure it does **NOT have a .txt** file extension.</span></span> <span data-ttu-id="0035a-518">Voir ci-dessous pour référence :</span><span class="sxs-lookup"><span data-stu-id="0035a-518">See below for reference:</span></span>
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

3.  <span data-ttu-id="0035a-520">Connectez-vous au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0035a-520">Log in to the [Azure Portal](https://portal.azure.com).</span></span>

4.  <span data-ttu-id="0035a-521">Une fois que vous êtes connecté, cliquez sur **créer une ressource** dans le coin supérieur gauche et recherchez **Function App**, puis appuyez sur la touche **entrée** pour effectuer la recherche.</span><span class="sxs-lookup"><span data-stu-id="0035a-521">Once you are logged in, click on **Create a resource** in the top left corner, and search for **Function App**, and press the **Enter** key, to search.</span></span> <span data-ttu-id="0035a-522">Cliquez sur *Function App* dans les résultats pour ouvrir un nouveau panneau.</span><span class="sxs-lookup"><span data-stu-id="0035a-522">Click *Function App* from the results, to open a new panel.</span></span>

    ![Rechercher une application de fonction](images/AzureLabs-Lab313-53.png)

5.  <span data-ttu-id="0035a-524">Le nouveau panneau fournit une description du service **Function App** .</span><span class="sxs-lookup"><span data-stu-id="0035a-524">The new panel will provide a description of the **Function App** Service.</span></span> <span data-ttu-id="0035a-525">En bas à gauche de ce panneau, cliquez sur le bouton **créer** pour créer une association avec ce service.</span><span class="sxs-lookup"><span data-stu-id="0035a-525">At the bottom left of this panel, click the **Create** button, to create an association with this Service.</span></span>

    ![instance de l’application de fonction](images/AzureLabs-Lab313-54.png)

6.  <span data-ttu-id="0035a-527">Une fois que vous avez cliqué sur **créer**, renseignez les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0035a-527">Once you have clicked on **Create**, fill in the following:</span></span>

    1. <span data-ttu-id="0035a-528">Pour **nom**de l’application, insérez le nom de votre choix pour cette instance de service.</span><span class="sxs-lookup"><span data-stu-id="0035a-528">For **App name**, insert your desired name for this Service instance.</span></span>

    2. <span data-ttu-id="0035a-529">Sélectionnez un **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="0035a-529">Select a **Subscription**.</span></span>

    3. <span data-ttu-id="0035a-530">Sélectionnez le niveau tarifaire approprié, s’il s’agit de la première fois que vous créez un **Service Function App**, vous devez disposer d’un niveau gratuit.</span><span class="sxs-lookup"><span data-stu-id="0035a-530">Select the pricing tier appropriate for you, if this is the first time creating a **Function App Service**, a free tier should be available to you.</span></span>

    4. <span data-ttu-id="0035a-531">Choisissez un **groupe de ressources** ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="0035a-531">Choose a **Resource Group** or create a new one.</span></span> <span data-ttu-id="0035a-532">Un groupe de ressources permet de surveiller, de contrôler l’accès, de configurer et de gérer la facturation d’un regroupement de ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0035a-532">A resource group provides a way to monitor, control access, provision, and manage, billing for a collection of Azure assets.</span></span> <span data-ttu-id="0035a-533">Il est recommandé de conserver tous les services Azure associés à un seul projet (par exemple, ces cours) dans un groupe de ressources commun.</span><span class="sxs-lookup"><span data-stu-id="0035a-533">It is recommended to keep all the Azure Services associated with a single project (e.g. such as these courses) under a common resource group).</span></span>

        > <span data-ttu-id="0035a-534">Si vous souhaitez en savoir plus sur les groupes de ressources Azure, cliquez [sur le lien suivant pour gérer un groupe de ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span><span class="sxs-lookup"><span data-stu-id="0035a-534">If you wish to read more about Azure Resource Groups, please follow this [link on how to manage a Resource Group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>

    5. <span data-ttu-id="0035a-535">Pour **système d’exploitation**, cliquez sur Windows, car il s’agit de la plateforme prévue.</span><span class="sxs-lookup"><span data-stu-id="0035a-535">For **OS**, click Windows, as that is the intended platform.</span></span>

    6. <span data-ttu-id="0035a-536">Sélectionnez un **plan d’hébergement** (ce didacticiel utilise un **plan de consommation**.</span><span class="sxs-lookup"><span data-stu-id="0035a-536">Select a **Hosting Plan** (this tutorial is using a **Consumption Plan**.</span></span>

    7. <span data-ttu-id="0035a-537">Sélectionnez un **emplacement** (choisissez le même emplacement que celui du stockage que vous avez créé à l’étape précédente)</span><span class="sxs-lookup"><span data-stu-id="0035a-537">Select a **Location** (choose the same location as the storage you have built in the previous step)</span></span>

    8. <span data-ttu-id="0035a-538">Pour la section **stockage** , **vous devez sélectionner le service de stockage que vous avez créé à l’étape précédente**.</span><span class="sxs-lookup"><span data-stu-id="0035a-538">For the **Storage** section, **you must select the Storage Service you created in the previous step**.</span></span>

    9. <span data-ttu-id="0035a-539">Vous n’aurez pas besoin de *application Insights* dans cette **application. n'** hésitez donc pas à la conserver.</span><span class="sxs-lookup"><span data-stu-id="0035a-539">You will not need *Application Insights* in this app, so feel free to leave it **Off**.</span></span>

    10. <span data-ttu-id="0035a-540">Cliquez sur **Create (Créer)** .</span><span class="sxs-lookup"><span data-stu-id="0035a-540">Click **Create**.</span></span>

        ![créer une nouvelle instance](images/AzureLabs-Lab313-55.png)

7.  <span data-ttu-id="0035a-542">Une fois que vous avez cliqué sur **créer**, vous devez attendre que le service soit créé, cette opération peut prendre une minute.</span><span class="sxs-lookup"><span data-stu-id="0035a-542">Once you have clicked on **Create**, you will have to wait for the Service to be created, this might take a minute.</span></span>

8.  <span data-ttu-id="0035a-543">Une notification s’affichera dans le portail une fois l’instance de service créée.</span><span class="sxs-lookup"><span data-stu-id="0035a-543">A notification will appear in the Portal once the Service instance is created.</span></span>

    ![nouvelle notification](images/AzureLabs-Lab313-56.png)

9.  <span data-ttu-id="0035a-545">Cliquez sur la notification, une fois le déploiement réussi (terminé).</span><span class="sxs-lookup"><span data-stu-id="0035a-545">Click on the notification, once deployment is successful (has finished).</span></span>

10. <span data-ttu-id="0035a-546">Cliquez sur le bouton **atteindre la ressource** dans la notification pour explorer votre nouvelle instance de service.</span><span class="sxs-lookup"><span data-stu-id="0035a-546">Click the **Go to resource** button in the notification to explore your new Service instance.</span></span> 

    ![accéder à la ressource](images/AzureLabs-Lab313-57.png)

11. <span data-ttu-id="0035a-548">Sur le côté gauche du nouveau panneau, cliquez sur l’icône **+** (plus) en regard de *fonctions*pour créer une fonction.</span><span class="sxs-lookup"><span data-stu-id="0035a-548">In the left side of the new panel, click the **+** (plus) icon next to *Functions*, to create a new function.</span></span>

    ![Ajouter une nouvelle fonction](images/AzureLabs-Lab313-58.png)

12. <span data-ttu-id="0035a-550">Dans le panneau central, la fenêtre de création de **fonction** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0035a-550">Within the central panel, the **Function** creation window will appear.</span></span> <span data-ttu-id="0035a-551">Faites défiler vers le dessous, puis cliquez sur **fonction personnalisée**.</span><span class="sxs-lookup"><span data-stu-id="0035a-551">Scroll down further, and click on **Custom function**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-59.png)

13. <span data-ttu-id="0035a-553">Faites défiler la page suivante jusqu’à ce que vous trouviez **IOT Hub (Event Hub)** , puis cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="0035a-553">Scroll down the next page, until you find **IoT Hub (Event Hub)**, then click on it.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-60.png)

14. <span data-ttu-id="0035a-555">Dans le panneau **IOT Hub (Event Hub)** , définissez la **langue** **C#** sur, puis cliquez sur **nouveau**.</span><span class="sxs-lookup"><span data-stu-id="0035a-555">In the **IoT Hub (Event Hub)** blade, set the **Language** to **C#** and then click on **new**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-61.png)

15. <span data-ttu-id="0035a-557">Dans la fenêtre qui s’affiche, assurez-vous que **IOT Hub** est sélectionné et que le nom du champ *IOT Hub* correspond au nom de votre *service IOT Hub* que vous avez créé précédemment ([à l’étape 8, du chapitre 3](#chapter-3---the-iot-hub-service)).</span><span class="sxs-lookup"><span data-stu-id="0035a-557">In the window that will appear, make sure that **IoT Hub** is selected and the name of the *IoT Hub* field corresponds with the name of your *IoT Hub Service* that you have created previously ([in step 8, of Chapter 3](#chapter-3---the-iot-hub-service)).</span></span> <span data-ttu-id="0035a-558">Cliquez ensuite sur le bouton **Sélectionner** .</span><span class="sxs-lookup"><span data-stu-id="0035a-558">Then click the **Select** button.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-62.png)

16. <span data-ttu-id="0035a-560">De retour dans le panneau **IOT Hub (Event Hub)** , cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-560">Back on the **IoT Hub (Event Hub)** blade, click on **Create**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-63.png)

17. <span data-ttu-id="0035a-562">Vous serez redirigé vers l’éditeur de fonction.</span><span class="sxs-lookup"><span data-stu-id="0035a-562">You will be redirected to the function editor.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-64.png)

18. <span data-ttu-id="0035a-564">Supprimez tout le code qu’il contient et remplacez-le par ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="0035a-564">Delete all the code in it and replace it with the following:</span></span>

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

19. <span data-ttu-id="0035a-565">Modifiez les variables suivantes pour qu’elles correspondent aux valeurs appropriées (**tables** et valeurs de **stockage** , [respectivement des étapes 11 et 13 du chapitre 11](#chapter-11---create-table-service)), que vous trouverez dans votre **compte de stockage**:</span><span class="sxs-lookup"><span data-stu-id="0035a-565">Change the following variables, so that they correspond to the appropriate values (**Table** and **Storage** values, from [step 11 and 13, respectively, of Chapter 11](#chapter-11---create-table-service)), that you will find in your **Storage Account**:</span></span>

    - <span data-ttu-id="0035a-566">**TableName**, avec le nom de votre **table** située dans votre **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0035a-566">**tableName**, with the name of your **Table** located in your **Storage Account**.</span></span>
    - <span data-ttu-id="0035a-567">**tableURL**, avec l’URL de votre **table** située dans votre **compte de stockage**.</span><span class="sxs-lookup"><span data-stu-id="0035a-567">**tableURL**, with the URL of your **Table** located in your **Storage Account**.</span></span>
    - <span data-ttu-id="0035a-568">**storageAccountName**, avec le nom de la valeur correspondant au nom de votre **compte de stockage** .</span><span class="sxs-lookup"><span data-stu-id="0035a-568">**storageAccountName**, with the name of the value corresponding with the name of your **Storage Account** name.</span></span>
    - <span data-ttu-id="0035a-569">**storageAccountKey**, avec la clé que vous avez obtenue dans le service de stockage que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="0035a-569">**storageAccountKey**, with the Key you have obtained in the Storage Service you have created previously.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-65.png)

20. <span data-ttu-id="0035a-571">Avec le code en place, cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-571">With the code in place, click **Save**.</span></span>

21. <span data-ttu-id="0035a-572">Ensuite, cliquez sur l’icône de **\<** (flèche), sur le côté droit de la page.</span><span class="sxs-lookup"><span data-stu-id="0035a-572">Next, click the **\<** (arrow) icon, on the right-hand side of the page.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-66.png)

22. <span data-ttu-id="0035a-574">Un panneau s’affiche à partir de la droite.</span><span class="sxs-lookup"><span data-stu-id="0035a-574">A panel will slide in from the right.</span></span> <span data-ttu-id="0035a-575">Dans ce panneau, cliquez sur **Télécharger**et un *Explorateur de fichiers* s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0035a-575">In that panel, click **Upload**, and a *File Browser* will appear.</span></span>

23. <span data-ttu-id="0035a-576">Accédez à, puis cliquez sur le fichier **Project. JSON** que vous avez créé précédemment dans le **bloc-notes** , puis cliquez sur le bouton **ouvrir** .</span><span class="sxs-lookup"><span data-stu-id="0035a-576">Navigate to, and click, the **project.json** file, which you created in **Notepad** previously, and then click the **Open** button.</span></span> <span data-ttu-id="0035a-577">Ce fichier définit les bibliothèques que votre fonction utilisera.</span><span class="sxs-lookup"><span data-stu-id="0035a-577">This file defines the libraries that your function will use.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-67.png)

24. <span data-ttu-id="0035a-579">Une fois le fichier chargé, il s’affiche dans le volet de droite.</span><span class="sxs-lookup"><span data-stu-id="0035a-579">When the file has uploaded, it will appear in the panel on the right.</span></span> <span data-ttu-id="0035a-580">Cliquez dessus pour l’ouvrir dans l’éditeur de **fonctions** .</span><span class="sxs-lookup"><span data-stu-id="0035a-580">Clicking it will open it within the **Function** editor.</span></span> <span data-ttu-id="0035a-581">Elle doit ressembler **exactement** à l’image suivante.</span><span class="sxs-lookup"><span data-stu-id="0035a-581">It must look **exactly** the same as the next image.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-68.png)

25. <span data-ttu-id="0035a-583">À ce stade, il serait judicieux de tester la capacité de votre fonction à stocker le message sur votre *table*.</span><span class="sxs-lookup"><span data-stu-id="0035a-583">At this point it would be good to test the capability of your Function to store the message on your *Table*.</span></span> <span data-ttu-id="0035a-584">Dans la partie supérieure droite de la fenêtre, cliquez sur **test**.</span><span class="sxs-lookup"><span data-stu-id="0035a-584">On the top right side of the window, click on **Test**.</span></span>

    ![fonction personnalisée](images/AzureLabs-Lab313-69.png)

26. <span data-ttu-id="0035a-586">Insérez un message dans le **corps**de la demande, comme indiqué dans l’image ci-dessus, puis cliquez sur **exécuter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-586">Insert a message on the **Request body**, as shown in the image above, and click on **Run**.</span></span> 

27. <span data-ttu-id="0035a-587">La fonction s’exécute et affiche l’état du résultat (vous remarquerez que l' **état vert 202 est accepté**, au-dessus de la fenêtre *sortie* , ce qui signifie qu’il s’agit d’un appel réussi) :</span><span class="sxs-lookup"><span data-stu-id="0035a-587">The function will run, displaying the result status (you will notice the green **Status 202 Accepted**, above the *Output* window, which means it was a successful call):</span></span>

    ![résultat de sortie](images/AzureLabs-Lab313-70.png)

## <a name="chapter-14---view-active-messages"></a><span data-ttu-id="0035a-589">Chapitre 14-afficher les messages actifs</span><span class="sxs-lookup"><span data-stu-id="0035a-589">Chapter 14 - View active messages</span></span>

<span data-ttu-id="0035a-590">Si vous ouvrez maintenant Visual Studio (**pas** Visual Studio code), vous pouvez visualiser le résultat de votre message de test, car il sera stocké dans la zone de chaîne *MessageContent* .</span><span class="sxs-lookup"><span data-stu-id="0035a-590">If you now open Visual Studio (**not** Visual Studio Code), you can visualize your test message result, as it will be stored in the *MessageContent* string area.</span></span>

![fonction personnalisée](images/AzureLabs-Lab313-71.png)

<span data-ttu-id="0035a-592">Une fois le service de table et le Function App en place, vos messages d’appareil Ubuntu s’affichent dans votre table *IoTMessages* .</span><span class="sxs-lookup"><span data-stu-id="0035a-592">With the Table Service and Function App in place, your Ubuntu device messages will appear in your *IoTMessages* Table.</span></span> <span data-ttu-id="0035a-593">S’il n’est pas déjà en cours d’exécution, redémarrez votre appareil et vous pourrez voir les messages de résultats de votre appareil et du module dans votre table, à l’aide de Visual Studio *Cloud Explorer*.</span><span class="sxs-lookup"><span data-stu-id="0035a-593">If not already running, start your device again, and you will be able to see the result messages from your device, and module, within your Table, through using Visual Studio *Cloud Explorer*.</span></span>

![visualiser les données](images/AzureLabs-Lab313-72.png)


## <a name="chapter-15---power-bi-setup"></a><span data-ttu-id="0035a-595">Chapitre 15-configuration de Power BI</span><span class="sxs-lookup"><span data-stu-id="0035a-595">Chapter 15 - Power BI Setup</span></span>

<span data-ttu-id="0035a-596">Pour visualiser les données de votre appareil IOT, vous allez configurer **Power bi** (version de bureau) pour collecter les données à partir du service de *table* , que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="0035a-596">To visualize the data from your IOT device you will setup **Power BI** (desktop version), to collect the data from the *Table* Service, which you just created.</span></span> <span data-ttu-id="0035a-597">La version *HoloLens* de Power bi utilisera ensuite ces données pour visualiser le résultat.</span><span class="sxs-lookup"><span data-stu-id="0035a-597">The *HoloLens* version of Power BI will then use that data to visualize the result.</span></span>

1.  <span data-ttu-id="0035a-598">Ouvrez la Microsoft Store sur Windows 10 et recherchez **Power bi Desktop**.</span><span class="sxs-lookup"><span data-stu-id="0035a-598">Open the Microsoft Store on Windows 10 and search for **Power BI Desktop**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-73.png)

2.  <span data-ttu-id="0035a-600">Téléchargez l’application.</span><span class="sxs-lookup"><span data-stu-id="0035a-600">Download the application.</span></span> <span data-ttu-id="0035a-601">Une fois le téléchargement terminé, ouvrez-le.</span><span class="sxs-lookup"><span data-stu-id="0035a-601">Once it has finished downloading, open it.</span></span>

3.  <span data-ttu-id="0035a-602">Connectez-vous à *Power bi* avec votre **compte Microsoft 365**.</span><span class="sxs-lookup"><span data-stu-id="0035a-602">Log into *Power BI* with your **Microsoft 365 account**.</span></span> <span data-ttu-id="0035a-603">Vous pouvez être redirigé vers un navigateur pour vous inscrire.</span><span class="sxs-lookup"><span data-stu-id="0035a-603">You may be redirected to a browser, to sign up.</span></span> <span data-ttu-id="0035a-604">Une fois que vous êtes inscrit, revenez à l’application Power BI, puis reconnectez-vous.</span><span class="sxs-lookup"><span data-stu-id="0035a-604">Once you are signed up, go back to the Power BI app, and sign in again.</span></span>

4.  <span data-ttu-id="0035a-605">Cliquez sur **obtenir des données** , puis cliquez sur **plus...** .</span><span class="sxs-lookup"><span data-stu-id="0035a-605">Click on **Get Data** and then click on **More...**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-74.png)

5.  <span data-ttu-id="0035a-607">Cliquez sur **Azure**, **stockage table Azure**, puis sur **se connecter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-607">Click **Azure**, **Azure Table Storage**, then click on **Connect**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-75.png)

6.  <span data-ttu-id="0035a-609">Vous serez invité à insérer l’URL de **table** que vous avez collectée précédemment ([à l’étape 13 du chapitre 11](#chapter-11---create-table-service)), lors de la création de votre service de table.</span><span class="sxs-lookup"><span data-stu-id="0035a-609">You will be prompted to insert the **Table URL** that you collected earlier ([in step 13 of Chapter 11](#chapter-11---create-table-service)), while creating your Table Service.</span></span> <span data-ttu-id="0035a-610">Après avoir inséré l’URL, supprimez la partie du chemin d’accès qui fait référence au sous-dossier de la table (qui était IoTMessages, dans ce cours).</span><span class="sxs-lookup"><span data-stu-id="0035a-610">After inserting the URL, delete the portion of the path referring to the Table "sub-folder" (which was IoTMessages, in this course).</span></span> <span data-ttu-id="0035a-611">Le résultat final doit être affiché dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0035a-611">The final result should be as displayed in the image below.</span></span> <span data-ttu-id="0035a-612">Cliquez ensuite sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0035a-612">Then click on **OK**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-76.png)

7.  <span data-ttu-id="0035a-614">Vous serez invité à insérer la clé de **stockage** que vous avez notée ([à l’étape 11 du chapitre 11](#chapter-11---create-table-service)) plus tôt lors de la création de votre stockage de table.</span><span class="sxs-lookup"><span data-stu-id="0035a-614">You will be prompted to insert the **Storage Key** that you noted ([in step 11 of Chapter 11](#chapter-11---create-table-service)) earlier while creating your Table Storage.</span></span> <span data-ttu-id="0035a-615">Cliquez ensuite sur **se connecter**.</span><span class="sxs-lookup"><span data-stu-id="0035a-615">Then click on **Connect**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-77.png)  

8. <span data-ttu-id="0035a-617">Un **panneau de navigation** s’affiche. cochez la case en regard de votre table, puis cliquez sur **charger**.</span><span class="sxs-lookup"><span data-stu-id="0035a-617">A **Navigator Panel** will be displayed, tick the box next to your Table and click on **Load**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-78.png)  

9. <span data-ttu-id="0035a-619">Votre table est maintenant chargée sur Power BI, mais elle nécessite une requête pour afficher les valeurs qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="0035a-619">Your table has now been loaded on Power BI, but it requires a query to display the values in it.</span></span> <span data-ttu-id="0035a-620">Pour ce faire, cliquez avec le bouton droit sur le nom de la table situé dans le **volet champs** sur le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="0035a-620">To do so, right-click on the table name located in the **FIELDS panel** at the right side of the screen.</span></span> <span data-ttu-id="0035a-621">Cliquez ensuite sur **modifier la requête**.</span><span class="sxs-lookup"><span data-stu-id="0035a-621">Then click on **Edit Query**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-79.png) 

10. <span data-ttu-id="0035a-623">Un **éditeur de Power Query** s’ouvre en tant que nouvelle fenêtre, affichant votre tableau.</span><span class="sxs-lookup"><span data-stu-id="0035a-623">A **Power Query Editor**  will open up as a new window, displaying your table.</span></span> <span data-ttu-id="0035a-624">Cliquez sur l' **enregistrement** Word dans la colonne *contenu* de la table pour visualiser le contenu stocké.</span><span class="sxs-lookup"><span data-stu-id="0035a-624">Click on the word **Record** within the *Content* column of the table, to visualize your stored content.</span></span>

    ![Power BI](images/AzureLabs-Lab313-80.png)    

11. <span data-ttu-id="0035a-626">Cliquez sur dans le **tableau**, en haut à gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0035a-626">Click on **Into Table**, at the top-left of the window.</span></span> 

    ![Power BI](images/AzureLabs-Lab313-81.png)

12. <span data-ttu-id="0035a-628">Cliquez sur **fermer & appliquer**.</span><span class="sxs-lookup"><span data-stu-id="0035a-628">Click on **Close & Apply**.</span></span>

    ![Power BI](images/AzureLabs-Lab313-82.png)

13. <span data-ttu-id="0035a-630">Une fois que le chargement de la requête est terminé, dans le **volet champs**, sur le côté droit de l’écran, cochez les cases correspondant aux paramètres **nom** et **valeur**, pour visualiser le contenu de la colonne **MessageContent** .</span><span class="sxs-lookup"><span data-stu-id="0035a-630">Once it has finished loading the query, within the **FIELDS panel**, on the right side of the screen, tick the boxes corresponding to the parameters **Name** and **Value**, to visualize the **MessageContent** column content.</span></span>

    ![Power BI](images/AzureLabs-Lab313-83.png)

14. <span data-ttu-id="0035a-632">Cliquez sur l' **icône de disque bleu** en haut à gauche de la fenêtre pour enregistrer votre travail dans un dossier de votre choix.</span><span class="sxs-lookup"><span data-stu-id="0035a-632">Click on the **blue disk icon** at the top left of the window to save your work in a folder of your choice.</span></span>

    ![Power BI](images/AzureLabs-Lab313-84.png)

15. <span data-ttu-id="0035a-634">Vous pouvez maintenant cliquer sur le bouton publier pour charger votre table dans votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="0035a-634">You can now click on the Publish button to upload your table to your Workspace.</span></span> <span data-ttu-id="0035a-635">Lorsque vous y êtes invité, cliquez sur **mon espace de travail** , puis sur *Sélectionner*.</span><span class="sxs-lookup"><span data-stu-id="0035a-635">When prompted, click **My workspace** and click *Select*.</span></span> <span data-ttu-id="0035a-636">Attendez qu’il affiche le résultat réussi de la soumission.</span><span class="sxs-lookup"><span data-stu-id="0035a-636">Wait for it to display the successful result of the submission.</span></span>

    ![Power BI](images/AzureLabs-Lab313-85.png)

    ![Power BI](images/AzureLabs-Lab313-86.png)

> [!WARNING]
> <span data-ttu-id="0035a-639">Le chapitre suivant est spécifique à HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0035a-639">The following Chapter is HoloLens specific.</span></span> <span data-ttu-id="0035a-640">Power BI n’est actuellement pas disponible en tant qu’application immersif, vous pouvez néanmoins exécuter la version de bureau dans le portail Windows Mixed Reality (également appelé maison), à l’aide de l’application de bureau.</span><span class="sxs-lookup"><span data-stu-id="0035a-640">Power BI is not currently available as an immersive application, however you can run the desktop version in the Windows Mixed Reality Portal (aka Cliff House), through the Desktop app.</span></span>

## <a name="chapter-16---display-power-bi-data-on-hololens"></a><span data-ttu-id="0035a-641">Chapitre 16-afficher les données de Power BI sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="0035a-641">Chapter 16 - Display Power BI data on HoloLens</span></span>

1. <span data-ttu-id="0035a-642">Sur votre HoloLens, connectez-vous au **Microsoft Store**, en appuyant sur son icône dans la liste des applications.</span><span class="sxs-lookup"><span data-stu-id="0035a-642">On your HoloLens, log in to the **Microsoft Store**, by tapping on its icon in the applications list.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-87.png)

2. <span data-ttu-id="0035a-644">Recherchez, puis téléchargez l’application **Power bi** .</span><span class="sxs-lookup"><span data-stu-id="0035a-644">Search and then download the **Power BI** application.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-88.png)

3. <span data-ttu-id="0035a-646">Démarrez **Power bi** à partir de votre liste d’applications.</span><span class="sxs-lookup"><span data-stu-id="0035a-646">Start **Power BI** from your applications list.</span></span> 

4. <span data-ttu-id="0035a-647">**Power bi** pouvez vous demander de vous connecter à votre **compte Microsoft 365**.</span><span class="sxs-lookup"><span data-stu-id="0035a-647">**Power BI** might ask you to login to your **Microsoft 365 account**.</span></span>

5. <span data-ttu-id="0035a-648">Une fois à l’intérieur de l’application, l’espace de travail doit s’afficher par défaut comme indiqué dans l’image ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0035a-648">Once inside the app, the workspace should display by default as shown in the image below.</span></span> <span data-ttu-id="0035a-649">Si cela ne se produit pas, cliquez simplement sur l’icône de l’espace de travail sur le côté gauche de la fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0035a-649">If that does not happen, simply click on the workspace icon on the left side of the window.</span></span>

    ![Power BI HL](images/AzureLabs-Lab313-89.png)

## <a name="your-finished-your-iot-hub-application"></a><span data-ttu-id="0035a-651">Votre application IoT Hub est terminée</span><span class="sxs-lookup"><span data-stu-id="0035a-651">Your finished your IoT Hub application</span></span>

<span data-ttu-id="0035a-652">Félicitations, vous avez créé avec succès un service IoT Hub, avec un appareil de périphérie de machine virtuelle simulé.</span><span class="sxs-lookup"><span data-stu-id="0035a-652">Congratulations, you have successfully created an IoT Hub Service, with a simulated Virtual Machine Edge device.</span></span> <span data-ttu-id="0035a-653">Votre appareil peut communiquer les résultats d’un modèle de Machine Learning à un service de table Azure, facilité par un Function App Azure, qui est lu dans Power BI et visualisé dans un Microsoft HoloLens.</span><span class="sxs-lookup"><span data-stu-id="0035a-653">Your device can  communicate the results of a machine learning model to an Azure Table Service, facilitated by an Azure Function App, which is read into Power BI, and visualized within a Microsoft HoloLens.</span></span>
 
![Power BI](images/AzureLabs-Lab313-00.png)

## <a name="bonus-exercises"></a><span data-ttu-id="0035a-655">Exercices bonus</span><span class="sxs-lookup"><span data-stu-id="0035a-655">Bonus exercises</span></span>

### <a name="exercise-1"></a><span data-ttu-id="0035a-656">Exercice 1</span><span class="sxs-lookup"><span data-stu-id="0035a-656">Exercise 1</span></span>

<span data-ttu-id="0035a-657">Développez la structure de messagerie stockée dans la table et affichez-la sous forme de graphique.</span><span class="sxs-lookup"><span data-stu-id="0035a-657">Expand the messaging structure stored in the table and display it as a graph.</span></span> <span data-ttu-id="0035a-658">Vous souhaiterez peut-être collecter davantage de données et les stocker dans la même table, pour les afficher ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="0035a-658">You might want to collect more data and store it in the same table, to be later displayed.</span></span>

### <a name="exercise-2"></a><span data-ttu-id="0035a-659">Exercice 2</span><span class="sxs-lookup"><span data-stu-id="0035a-659">Exercise 2</span></span>

<span data-ttu-id="0035a-660">Créez un module « capture d’appareil photo » supplémentaire à déployer sur le tableau IoT, afin qu’il puisse capturer des images via l’appareil photo à analyser.</span><span class="sxs-lookup"><span data-stu-id="0035a-660">Create an additional "camera capture" module to be deployed on the IoT board, so that it can capture images through the camera to be analyzed.</span></span>
