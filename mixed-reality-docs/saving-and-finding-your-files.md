---
title: Enregistrement et recherche de vos fichiers
description: Comment rechercher, enregistrer et partager des fichiers sur HoloLens.
author: mattzmsft
ms.author: mazeller
ms.date: 09/27/2018
ms.topic: article
keywords: procédures, sélecteur de fichiers, fichiers, photos, vidéos, images, OneDrive, stockage, Explorateur de fichiers
ms.openlocfilehash: d539af29fc94fdbde0d2cf08157ae8b5ce8ad0a1
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63524601"
---
# <a name="saving-and-finding-your-files"></a><span data-ttu-id="87fe8-104">Enregistrement et recherche de vos fichiers</span><span class="sxs-lookup"><span data-stu-id="87fe8-104">Saving and finding your files</span></span>

<span data-ttu-id="87fe8-105">Les fichiers peuvent être enregistrés et gérés de la même façon que les autres appareils Windows 10 Desktop et mobile:</span><span class="sxs-lookup"><span data-stu-id="87fe8-105">Files can be saved and managed in a similar manner to other Windows 10 Desktop and Mobile devices:</span></span>
* <span data-ttu-id="87fe8-106">Utilisation de l’application Explorateur de fichiers pour accéder aux dossiers locaux</span><span class="sxs-lookup"><span data-stu-id="87fe8-106">Using the File Explorer app to access local folders</span></span>
* <span data-ttu-id="87fe8-107">Dans le propre stockage d’une application</span><span class="sxs-lookup"><span data-stu-id="87fe8-107">Within an app's own storage</span></span>
* <span data-ttu-id="87fe8-108">Dans un dossier connu spécial (tel que la bibliothèque vidéo ou musique)</span><span class="sxs-lookup"><span data-stu-id="87fe8-108">In a special known folder (such as the video or music library)</span></span>
* <span data-ttu-id="87fe8-109">Utilisation d’un service de stockage qui comprend un sélecteur d’application et de fichier (par exemple, OneDrive)</span><span class="sxs-lookup"><span data-stu-id="87fe8-109">Using a storage service that includes an app and file picker (such as OneDrive)</span></span>
* <span data-ttu-id="87fe8-110">Utilisation d’un PC de bureau connecté à votre HoloLens via USB via la prise en charge du protocole MTP (Media Transfer Protocol)</span><span class="sxs-lookup"><span data-stu-id="87fe8-110">Using a desktop PC connected to your HoloLens via USB, via MTP (Media Transfer Protocol) support</span></span>

## <a name="file-explorer"></a><span data-ttu-id="87fe8-111">Explorateur de fichiers</span><span class="sxs-lookup"><span data-stu-id="87fe8-111">File Explorer</span></span>

<span data-ttu-id="87fe8-112">Vous pouvez utiliser l’application Explorateur de fichiers pour déplacer et supprimer des fichiers à partir de HoloLens.</span><span class="sxs-lookup"><span data-stu-id="87fe8-112">You can use the File Explorer app to move and delete files from within HoloLens.</span></span>

>[!NOTE]
><span data-ttu-id="87fe8-113">Si vous ne voyez aucun fichier dans l’Explorateur de fichiers, le filtre «récent» peut être actif (l’icône d’horloge est mise en surbrillance dans le volet gauche).</span><span class="sxs-lookup"><span data-stu-id="87fe8-113">If you don’t see any files in File Explorer, the "Recent" filter may be active (clock icon is highlighted in left pane).</span></span> <span data-ttu-id="87fe8-114">Pour résoudre ce problème, sélectionnez l’icône de document de **ce périphérique** dans le volet gauche (sous l’icône d’horloge) ou ouvrez le menu et sélectionnez **cet appareil**.</span><span class="sxs-lookup"><span data-stu-id="87fe8-114">To fix this, select the **This Device** document icon in the left pane (beneath the clock icon), or open the menu and select **This Device**.</span></span>

## <a name="files-within-an-app"></a><span data-ttu-id="87fe8-115">Fichiers dans une application</span><span class="sxs-lookup"><span data-stu-id="87fe8-115">Files within an app</span></span>

<span data-ttu-id="87fe8-116">Si une application enregistre des fichiers sur votre appareil, vous pouvez utiliser cette application pour y accéder.</span><span class="sxs-lookup"><span data-stu-id="87fe8-116">If an application saves files on your device, you can use that application to access them.</span></span>

### <a name="where-are-my-photosvideos"></a><span data-ttu-id="87fe8-117">Où se trouvent mes photos/vidéos?</span><span class="sxs-lookup"><span data-stu-id="87fe8-117">Where are my photos/videos?</span></span>

<span data-ttu-id="87fe8-118">La [réalité mixte capture](mixed-reality-capture.md) des photos et des vidéos sont enregistrées dans le dossier pellicule de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="87fe8-118">[Mixed reality capture](mixed-reality-capture.md) photos and videos are saved to the device's Camera Roll folder.</span></span> <span data-ttu-id="87fe8-119">Vous pouvez y accéder via l' [application photos](see-your-photos.md#photos-app).</span><span class="sxs-lookup"><span data-stu-id="87fe8-119">These can be accessed via the [Photos app](see-your-photos.md#photos-app).</span></span> <span data-ttu-id="87fe8-120">Vous pouvez utiliser l’application photos pour synchroniser vos photos et vidéos sur OneDrive.</span><span class="sxs-lookup"><span data-stu-id="87fe8-120">You can use the Photos app to sync your photos and videos to OneDrive.</span></span> <span data-ttu-id="87fe8-121">Vous pouvez également accéder à vos photos et vidéos via la page de capture de la réalité mixte du [portail d’appareils Windows](using-the-windows-device-portal.md#mixed-reality-capture).</span><span class="sxs-lookup"><span data-stu-id="87fe8-121">You can also access your photos and videos via the Mixed Reality Capture page of the [Windows Device Portal](using-the-windows-device-portal.md#mixed-reality-capture).</span></span>

### <a name="requesting-files-from-another-app"></a><span data-ttu-id="87fe8-122">Demande de fichiers à partir d’une autre application</span><span class="sxs-lookup"><span data-stu-id="87fe8-122">Requesting files from another app</span></span>

<span data-ttu-id="87fe8-123">Une application peut demander l’enregistrement d’un fichier ou l’ouverture d’un fichier à partir d’une autre application via des sélecteurs de [fichiers](app-model.md#file-pickers).</span><span class="sxs-lookup"><span data-stu-id="87fe8-123">An application can request to save a file or open a file from another app via [file pickers](app-model.md#file-pickers).</span></span>

## <a name="known-folders"></a><span data-ttu-id="87fe8-124">Dossiers connus</span><span class="sxs-lookup"><span data-stu-id="87fe8-124">Known folders</span></span>

<span data-ttu-id="87fe8-125">HoloLens prend en charge un certain nombre de [dossiers connus](app-model.md#known-folders) auxquels les applications peuvent demander une autorisation d’accès.</span><span class="sxs-lookup"><span data-stu-id="87fe8-125">HoloLens supports a number of [known folders](app-model.md#known-folders) that apps can request permission to access.</span></span>

## <a name="files-in-a-service"></a><span data-ttu-id="87fe8-126">Fichiers dans un service</span><span class="sxs-lookup"><span data-stu-id="87fe8-126">Files in a service</span></span>

<span data-ttu-id="87fe8-127">Pour enregistrer un fichier dans (ou accéder aux fichiers à partir de) un service, l’application associée au service doit être installée.</span><span class="sxs-lookup"><span data-stu-id="87fe8-127">To save a file to (or access files from) a service, the app associated with the service has to be installed.</span></span> <span data-ttu-id="87fe8-128">Pour pouvoir enregistrer des fichiers dans et accéder à des fichiers à partir de OneDrive, vous devez installer l' [application onedrive](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3).</span><span class="sxs-lookup"><span data-stu-id="87fe8-128">In order to save files to and access files from OneDrive, you will need to install the [OneDrive app](https://www.microsoft.com/store/apps/onedrive/9wzdncrfj1p3).</span></span>

## <a name="mtp-media-transfer-protocol"></a><span data-ttu-id="87fe8-129">MTP (Media Transfer Protocol)</span><span class="sxs-lookup"><span data-stu-id="87fe8-129">MTP (Media Transfer Protocol)</span></span>

<span data-ttu-id="87fe8-130">À l’instar des autres appareils mobiles, connectez HoloLens à votre ordinateur de bureau et ouvrez l’Explorateur de fichiers sur le PC pour accéder à vos bibliothèques HoloLens (photos, vidéos, documents) en vue de les transférer facilement.</span><span class="sxs-lookup"><span data-stu-id="87fe8-130">Similar to other mobile devices, connect HoloLens to your desktop PC and open File Explorer on the PC to access your HoloLens libraries (photos, videos, documents) for easy transfer.</span></span>

## <a name="clarifications"></a><span data-ttu-id="87fe8-131">Éclaircissements</span><span class="sxs-lookup"><span data-stu-id="87fe8-131">Clarifications</span></span>

* <span data-ttu-id="87fe8-132">HoloLens ne prend pas en charge la connexion à des disques durs externes ou à des cartes SD.</span><span class="sxs-lookup"><span data-stu-id="87fe8-132">HoloLens does not support connecting to external hard drives or SD cards.</span></span>
* <span data-ttu-id="87fe8-133">À compter de la [mise à jour 2018 de Windows 10 avril (RS4) pour HoloLens](release-notes-april-2018.md), hololens comprend l’Explorateur de fichiers pour l’enregistrement et la gestion des fichiers sur-appareil.</span><span class="sxs-lookup"><span data-stu-id="87fe8-133">As of the [Windows 10 April 2018 Update (RS4) for HoloLens](release-notes-april-2018.md), HoloLens includes File Explorer for saving and managing files on-device.</span></span> <span data-ttu-id="87fe8-134">L’ajout de l’Explorateur de fichiers vous donne également la possibilité de choisir votre sélecteur de fichiers (par exemple, l’enregistrement d’un fichier sur votre appareil ou sur OneDrive).</span><span class="sxs-lookup"><span data-stu-id="87fe8-134">The addition of File Explorer also gives you the ability to choose your file picker (for example, saving a file to your device or to OneDrive).</span></span>
