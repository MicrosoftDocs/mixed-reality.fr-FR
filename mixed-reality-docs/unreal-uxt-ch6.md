---
title: 6. Empaquetage et déploiement sur un appareil ou un émulateur
description: Partie 6 d’un tutoriel pour créer une application de jeu d’échecs simple avec Unreal Engine 4 et le plug-in UX Tools du Mixed Reality Toolkit
author: sw5813
ms.author: suwu
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, tutoriel, bien démarrer, mrtk, uxt, UX Tools, documentation
ms.openlocfilehash: b3f0b5f9ca5347c337091539b1cc0e214515c989
ms.sourcegitcommit: 09d9fa153cd9072f60e33a5f83ced8167496fcd7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/18/2020
ms.locfileid: "83519964"
---
# <a name="6-packaging--deploying-to-device-or-emulator"></a><span data-ttu-id="63044-104">6. Empaquetage et déploiement sur un appareil ou un émulateur</span><span class="sxs-lookup"><span data-stu-id="63044-104">6. Packaging & deploying to device or emulator</span></span>

<span data-ttu-id="63044-105">Cette section vous guide dans les étapes de préparation de votre application pour qu’elle s’exécute sur un appareil ou un émulateur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="63044-105">This section walks you through the steps of preparing your app to run on a HoloLens 2 device or Emulator.</span></span> <span data-ttu-id="63044-106">Si vous disposez d’un appareil, vous pouvez effectuer un streaming depuis votre ordinateur vers le périphérique ou empaqueter l’application pour qu’elle s’exécute directement sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="63044-106">If you have a device, you can either stream from your computer to the device or package the app to run directly on the device.</span></span> <span data-ttu-id="63044-107">Si vous n’avez pas d’appareil, vous devez empaqueter l’application pour qu’elle s’exécute sur l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="63044-107">If you do not have a device, you will need to package the app for it to run on the Emulator.</span></span> 

## <a name="objectives"></a><span data-ttu-id="63044-108">Objectifs</span><span class="sxs-lookup"><span data-stu-id="63044-108">Objectives</span></span>

* <span data-ttu-id="63044-109">[Appareil uniquement] Streaming de votre application vers HoloLens 2 via l’exécution à distance d’une application holographique</span><span class="sxs-lookup"><span data-stu-id="63044-109">[Device only] Stream your app to HoloLens 2 via holographic app remoting</span></span>
* <span data-ttu-id="63044-110">Empaqueter et déployer votre application sur un appareil ou un émulateur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="63044-110">Package and deploy your app to a HoloLens 2 device or emulator</span></span>

## <a name="device-only-stream"></a><span data-ttu-id="63044-111">[Appareil uniquement] Streaming</span><span class="sxs-lookup"><span data-stu-id="63044-111">[Device Only] Stream</span></span>

1.  <span data-ttu-id="63044-112">Installez le **lecteur distant holographique** à partir du Microsoft Store sur votre HoloLens 2 et exécuter l’application</span><span class="sxs-lookup"><span data-stu-id="63044-112">Install the **Holographic Remoting Player** from the Microsoft Store on your HoloLens 2 and run the app</span></span>

2.  <span data-ttu-id="63044-113">Accédez à **Edit > Project Settings**.</span><span class="sxs-lookup"><span data-stu-id="63044-113">Go to **Edit > Project Settings**.</span></span> <span data-ttu-id="63044-114">Dans la section Holographic Remoting, cochez la case pour activer la communication à distance, puis redémarrez l’éditeur.</span><span class="sxs-lookup"><span data-stu-id="63044-114">In the Holographic Remoting section, check the box to enable remoting and restart the editor.</span></span>

3.  <span data-ttu-id="63044-115">Entrez l’adresse IP de votre appareil, puis cliquez sur Connect.</span><span class="sxs-lookup"><span data-stu-id="63044-115">Input the IP address of your device and click Connect.</span></span>

4.  <span data-ttu-id="63044-116">Une fois que vous êtes connecté, dans votre éditeur UE4, cliquez sur la flèche déroulante à droite du bouton Play et sélectionnez VR Preview.</span><span class="sxs-lookup"><span data-stu-id="63044-116">Once you’re connected, in your UE4 Editor, click the drop-down arrow to the right of the Play button and select VR Preview.</span></span>

## <a name="package-and-deploy-your-app"></a><span data-ttu-id="63044-117">Empaqueter et déployer votre application</span><span class="sxs-lookup"><span data-stu-id="63044-117">Package and deploy your app</span></span> 

>[!NOTE]
><span data-ttu-id="63044-118">S’il s’agit de la première fois que vous empaquetez une application Unreal pour HoloLens, vous devrez télécharger les fichiers de prise en charge à partir de l’Epic Launcher.</span><span class="sxs-lookup"><span data-stu-id="63044-118">If this is your first time packaging an Unreal app for HoloLens, you'll need to download supporting files from the Epic Launcher.</span></span> <span data-ttu-id="63044-119">Pour ce faire, accédez à l’onglet **Library** dans l’Epic Games Launcher.</span><span class="sxs-lookup"><span data-stu-id="63044-119">To do so, go to the **Library** tab in the Epic Games Launcher.</span></span> <span data-ttu-id="63044-120">Sélectionnez la flèche déroulante à côté de **Launch** et sélectionnez **Options**.</span><span class="sxs-lookup"><span data-stu-id="63044-120">Select the dropdown arrow next to **Launch** and select **Options**.</span></span> <span data-ttu-id="63044-121">Sous **Target Platforms**, sélectionnez **HoloLens 2** et cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="63044-121">Under **Target Platforms**, select **HoloLens 2** and click **Apply**.</span></span> 
><span data-ttu-id="63044-122">![Paramètres du projet - Description](images/unreal-uxt/6-installationoptions.PNG)</span><span class="sxs-lookup"><span data-stu-id="63044-122">![Project Settings - Description](images/unreal-uxt/6-installationoptions.PNG)</span></span>

1.  <span data-ttu-id="63044-123">Accédez à **Edit > Project Settings**.</span><span class="sxs-lookup"><span data-stu-id="63044-123">Go to **Edit > Project Settings**.</span></span> <span data-ttu-id="63044-124">Sous **Project > Description > About > Project Name**, donnez un nom à votre projet.</span><span class="sxs-lookup"><span data-stu-id="63044-124">Under **Project > Description > About > Project Name**, give your project a name.</span></span> <span data-ttu-id="63044-125">Sous **Project > Description > Publisher > Company Distinguished Name**, placez « CN={INSERT COMPANY NAME} ».</span><span class="sxs-lookup"><span data-stu-id="63044-125">Under **Project > Description > Publisher > Company Distinguished Name** put “CN={INSERT COMPANY NAME}”.</span></span> <span data-ttu-id="63044-126">Si vous laissez un de ces champs vide, vous recevrez une erreur.</span><span class="sxs-lookup"><span data-stu-id="63044-126">Leaving either of these fields blank will result in an error.</span></span> 

![Paramètres du projet - Description](images/unreal-uxt/6-cn.PNG)

2.  <span data-ttu-id="63044-128">Sous **Platforms > HoloLens**, choisissez Emulation et/ou Device selon ce que vous voulez cibler.</span><span class="sxs-lookup"><span data-stu-id="63044-128">Under **Platforms > HoloLens** choose Emulation and/or Device based on which you want to target.</span></span>

3.  <span data-ttu-id="63044-129">Dans la section **Packaging**, en regard de **Signing Certificate**, cliquez sur le bouton **Generate new** pour générer un nouveau certificat de signature.</span><span class="sxs-lookup"><span data-stu-id="63044-129">In the **Packaging** section, next to **Signing Certificate**, click the **Generate new** button to generate a new signing certificate.</span></span> <span data-ttu-id="63044-130">Revenez dans la fenêtre principale.</span><span class="sxs-lookup"><span data-stu-id="63044-130">Return to the Main window.</span></span>

![Paramètres du projet - Plateformes - HoloLens](images/unreal-uxt/6-packaging.PNG)

4.  <span data-ttu-id="63044-132">Accédez à **File > Package Project** et sélectionnez **HoloLens**.</span><span class="sxs-lookup"><span data-stu-id="63044-132">Go to **File > Package Project** and select **HoloLens**.</span></span> <span data-ttu-id="63044-133">Créez un dossier où enregistrer votre package, puis cliquez sur **Select Folder**.</span><span class="sxs-lookup"><span data-stu-id="63044-133">Create a new folder to save your package in and click **Select Folder**.</span></span> 

5.  <span data-ttu-id="63044-134">Une fois que l’application a été empaquetée correctement, ouvrez le **Windows Device Portal**, accédez à **Views > Apps** et recherchez la section **Deploy apps**.</span><span class="sxs-lookup"><span data-stu-id="63044-134">Once the app has been successfully packaged, open the **Windows Device Portal**, go to **Views > Apps**, and find the **Deploy apps** section.</span></span>

6.  <span data-ttu-id="63044-135">Cliquez sur **Browse...** et accédez à votre fichier **ChessApp.appxbundle**.</span><span class="sxs-lookup"><span data-stu-id="63044-135">Click**Browse...** and navigate to your **ChessApp.appxbundle** file.</span></span> <span data-ttu-id="63044-136">Cliquez sur **Ouvrir**.</span><span class="sxs-lookup"><span data-stu-id="63044-136">Click **Open**.</span></span> 

    * <span data-ttu-id="63044-137">Si c’est la première fois que vous installez l’application sur votre appareil, cochez la case en regard de **Allow me to select framework packages**.</span><span class="sxs-lookup"><span data-stu-id="63044-137">If this is the first time you are installing the app on your device, check the box next to **Allow me to select framework packages**.</span></span> <span data-ttu-id="63044-138">Dans la boîte de dialogue suivante, incluez le fichier appx VCLibs approprié (arm64 pour l’appareil, x64 pour l’émulateur).</span><span class="sxs-lookup"><span data-stu-id="63044-138">In the next dialogue, include the appropriate VCLibs appx file (arm64 for device, x64 for emulator).</span></span> 

7.  <span data-ttu-id="63044-139">Cliquez sur **Install**.</span><span class="sxs-lookup"><span data-stu-id="63044-139">Click **Install**</span></span>

<span data-ttu-id="63044-140">Félicitations, vous avez terminé ce tutoriel !</span><span class="sxs-lookup"><span data-stu-id="63044-140">Congratulations on finishing this tutorial!</span></span>  