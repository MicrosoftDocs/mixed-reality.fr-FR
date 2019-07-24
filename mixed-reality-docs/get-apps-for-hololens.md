---
title: Obtenir des applications pour HoloLens
description: Décrit l’installation d’applications pour HoloLens, à la fois via le Microsoft Store et le chargement par le côté.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: chargement, charge latérale, chargement secondaire, Store, UWP, application, installer
ms.openlocfilehash: 5042c380e3a548e5001e045676190c2349a835a0
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63522566"
---
# <a name="get-apps-for-hololens"></a><span data-ttu-id="b3f58-104">Obtenir des applications pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="b3f58-104">Get apps for HoloLens</span></span>

<span data-ttu-id="b3f58-105">En tant qu’appareil Windows 10, HoloLens prend en charge de nombreuses applications UWP existantes à partir de l’App Store, ainsi que de nouvelles applications conçues spécifiquement pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b3f58-105">As a Windows 10 device, HoloLens supports many existing UWP applications from the app store, as well as new apps built specifically for HoloLens.</span></span> <span data-ttu-id="b3f58-106">En plus de ceux-ci, vous souhaiterez peut-être même [développer](development-overview.md) et installer vos propres applications ou celles de vos amis!</span><span class="sxs-lookup"><span data-stu-id="b3f58-106">On top of these, you may even want to [develop](development-overview.md) and install your own apps or those of your friends!</span></span>

## <a name="installing-apps"></a><span data-ttu-id="b3f58-107">Installation d’applications</span><span class="sxs-lookup"><span data-stu-id="b3f58-107">Installing Apps</span></span>

<span data-ttu-id="b3f58-108">Il existe trois façons d’installer de nouvelles applications sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b3f58-108">There are three ways to install new apps on your HoloLens.</span></span> <span data-ttu-id="b3f58-109">La méthode principale consiste à installer de nouvelles applications à partir du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="b3f58-109">The primary method will be to install new applications from the Windows Store.</span></span> <span data-ttu-id="b3f58-110">Toutefois, vous pouvez également installer vos propres applications à l’aide du portail des appareils ou en les déployant à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b3f58-110">However, you can also install your own applications using either the Device Portal or by deploying them from Visual Studio.</span></span>

### <a name="from-the-microsoft-store"></a><span data-ttu-id="b3f58-111">À partir de la Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="b3f58-111">From the Microsoft Store</span></span>
1. <span data-ttu-id="b3f58-112">Effectuez un mouvement de [floraison](gestures.md#bloom) pour ouvrir le [menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).</span><span class="sxs-lookup"><span data-stu-id="b3f58-112">Perform a [bloom](gestures.md#bloom) gesture to open the [Start Menu](navigating-the-windows-mixed-reality-home.md#start-menu).</span></span>
2. <span data-ttu-id="b3f58-113">Sélectionnez l’application du Store, puis appuyez pour placer cette vignette dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="b3f58-113">Select the Store app and then tap to place this tile into your world.</span></span>
3. <span data-ttu-id="b3f58-114">Une fois l’application du Store ouverte, utilisez la barre de recherche pour rechercher les applications souhaitées.</span><span class="sxs-lookup"><span data-stu-id="b3f58-114">Once the Store app opens, use the search bar to look for any desired application.</span></span>
4. <span data-ttu-id="b3f58-115">Sélectionnez **obtenir** ou **installer** sur la page de l’application (un achat peut être nécessaire).</span><span class="sxs-lookup"><span data-stu-id="b3f58-115">Select **Get** or **Install** on the application's page (a purchase may be required).</span></span>

### <a name="installing-an-application-package-with-the-device-portal"></a><span data-ttu-id="b3f58-116">Installation d’un package d’application avec le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="b3f58-116">Installing an application package with the Device Portal</span></span>
1. <span data-ttu-id="b3f58-117">Établissez une connexion entre le portail de l' [appareil](using-the-windows-device-portal.md) et le HoloLens cible.</span><span class="sxs-lookup"><span data-stu-id="b3f58-117">Establish a connection from [Device Portal](using-the-windows-device-portal.md) to the target HoloLens.</span></span>
2. <span data-ttu-id="b3f58-118">Accédez à la page **applications** dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="b3f58-118">Navigate to the **Apps** page in the left navigation.</span></span>
3. <span data-ttu-id="b3f58-119">Sous **package d’application** , accédez au fichier. AppX associé à votre application.</span><span class="sxs-lookup"><span data-stu-id="b3f58-119">Under **App Package** Browse to the .appx file associated with your application.</span></span>
  >[!IMPORTANT]
  ><span data-ttu-id="b3f58-120">Veillez à référencer les fichiers de dépendance et de certificat associés.</span><span class="sxs-lookup"><span data-stu-id="b3f58-120">Make sure to reference any associated dependency and certificate files.</span></span>

4. <span data-ttu-id="b3f58-121">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b3f58-121">Click **Go**.</span></span>

<span data-ttu-id="b3f58-122">![Installer le formulaire d’application dans le portail de périphériques Windows sur Microsoft HoloLens](images/deviceportal-appmanager.jpg)</span><span class="sxs-lookup"><span data-stu-id="b3f58-122">![Install app form in Windows Device Portal on Microsoft HoloLens](images/deviceportal-appmanager.jpg)</span></span><br>
<span data-ttu-id="b3f58-123">Utilisation du portail d’appareils Windows pour installer une application sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="b3f58-123">Using Windows Device Portal to install an app on HoloLens</span></span>

### <a name="deploying-from-microsoft-visual-studio-2015"></a><span data-ttu-id="b3f58-124">Déploiement à partir de Microsoft Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="b3f58-124">Deploying from Microsoft Visual Studio 2015</span></span>
1. <span data-ttu-id="b3f58-125">Ouvrez la solution Visual Studio de votre application (fichier. sln).</span><span class="sxs-lookup"><span data-stu-id="b3f58-125">Open your app's Visual Studio solution (.sln file).</span></span>
2. <span data-ttu-id="b3f58-126">Ouvrez les **Propriétés** du projet.</span><span class="sxs-lookup"><span data-stu-id="b3f58-126">Open the project's **Properties** .</span></span>
3. <span data-ttu-id="b3f58-127">Sélectionnez la configuration de build suivante: Ordinateur maître/x86/distant.</span><span class="sxs-lookup"><span data-stu-id="b3f58-127">Select the following build configuration: Master/x86/Remote Machine.</span></span>
4. <span data-ttu-id="b3f58-128">Lorsque vous sélectionnez ordinateur distant:</span><span class="sxs-lookup"><span data-stu-id="b3f58-128">When you select Remote Machine:</span></span>
   * <span data-ttu-id="b3f58-129">Assurez-vous que l’adresse pointe vers l’adresse IP WiFi de l’HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b3f58-129">Make sure the address points to the HoloLens' WiFi IP address.</span></span>
   * <span data-ttu-id="b3f58-130">Définissez authentification sur universel (protocole non chiffré).</span><span class="sxs-lookup"><span data-stu-id="b3f58-130">Set authentication to Universal (Unencrypted Protocol).</span></span>
5. <span data-ttu-id="b3f58-131">Générez votre solution.</span><span class="sxs-lookup"><span data-stu-id="b3f58-131">Build your solution.</span></span>
6. <span data-ttu-id="b3f58-132">Cliquez sur le bouton **ordinateur distant** pour déployer l’application à partir de votre PC de développement vers votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b3f58-132">Click the **Remote Machine** button to deploy the app from your development PC to your HoloLens.</span></span> <span data-ttu-id="b3f58-133">Si vous avez déjà une build existante sur HoloLens, sélectionnez Oui pour réinstaller cette version plus récente.</span><span class="sxs-lookup"><span data-stu-id="b3f58-133">If you already have an existing build on the HoloLens, select yes to re-install this newer version.</span></span><br>
  <span data-ttu-id="b3f58-134">![Déploiement d’ordinateurs distants pour des applications dans Microsoft HoloLens dans Visual Studio](images/vs2015-remotedeployment.jpg)</span><span class="sxs-lookup"><span data-stu-id="b3f58-134">![Remote Machine deployment for apps to Microsoft HoloLens in Visual Studio](images/vs2015-remotedeployment.jpg)</span></span><br>
7. <span data-ttu-id="b3f58-135">L’application s’installe et se lance automatiquement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="b3f58-135">The application will install and auto launch on your HoloLens.</span></span>
