---
title: Obtenez des applications pour HoloLens
description: Décrit l’installation d’applications pour HoloLens, à la fois via le Microsoft Store et le chargement indépendant.
author: mattzmsft
ms.author: mazeller
ms.date: 03/21/2018
ms.topic: article
keywords: chargement de version test, chargement indépendant, chargement indépendant, store, uwp, application, installer
ms.openlocfilehash: 5042c380e3a548e5001e045676190c2349a835a0
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59593247"
---
# <a name="get-apps-for-hololens"></a><span data-ttu-id="599bb-104">Obtenez des applications pour HoloLens</span><span class="sxs-lookup"><span data-stu-id="599bb-104">Get apps for HoloLens</span></span>

<span data-ttu-id="599bb-105">Un appareil Windows 10, HoloLens prend en charge de nombreuses applications UWP existantes à partir du magasin d’applications, ainsi que les nouvelles applications conçues spécialement pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-105">As a Windows 10 device, HoloLens supports many existing UWP applications from the app store, as well as new apps built specifically for HoloLens.</span></span> <span data-ttu-id="599bb-106">Sur ces ressources, vous pouvez également [développer](development-overview.md) et installer vos propres applications ou ceux de vos amis !</span><span class="sxs-lookup"><span data-stu-id="599bb-106">On top of these, you may even want to [develop](development-overview.md) and install your own apps or those of your friends!</span></span>

## <a name="installing-apps"></a><span data-ttu-id="599bb-107">Installation d’applications</span><span class="sxs-lookup"><span data-stu-id="599bb-107">Installing Apps</span></span>

<span data-ttu-id="599bb-108">Il existe trois façons d’installer de nouvelles applications sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-108">There are three ways to install new apps on your HoloLens.</span></span> <span data-ttu-id="599bb-109">La méthode principale sera d’installer de nouvelles applications à partir du Windows Store.</span><span class="sxs-lookup"><span data-stu-id="599bb-109">The primary method will be to install new applications from the Windows Store.</span></span> <span data-ttu-id="599bb-110">Toutefois, vous pouvez également installer vos propres applications via le portail de l’appareil ou en les déployant à partir de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="599bb-110">However, you can also install your own applications using either the Device Portal or by deploying them from Visual Studio.</span></span>

### <a name="from-the-microsoft-store"></a><span data-ttu-id="599bb-111">À partir du Microsoft Store</span><span class="sxs-lookup"><span data-stu-id="599bb-111">From the Microsoft Store</span></span>
1. <span data-ttu-id="599bb-112">Effectuer un [bloom](gestures.md#bloom) mouvement pour ouvrir le [Menu Démarrer](navigating-the-windows-mixed-reality-home.md#start-menu).</span><span class="sxs-lookup"><span data-stu-id="599bb-112">Perform a [bloom](gestures.md#bloom) gesture to open the [Start Menu](navigating-the-windows-mixed-reality-home.md#start-menu).</span></span>
2. <span data-ttu-id="599bb-113">Sélectionnez l’application de Store, puis sur pour placer cette vignette dans votre monde.</span><span class="sxs-lookup"><span data-stu-id="599bb-113">Select the Store app and then tap to place this tile into your world.</span></span>
3. <span data-ttu-id="599bb-114">Une fois que l’application de Store s’ouvre, utilisez la barre de recherche pour rechercher n’importe quelle application souhaitée.</span><span class="sxs-lookup"><span data-stu-id="599bb-114">Once the Store app opens, use the search bar to look for any desired application.</span></span>
4. <span data-ttu-id="599bb-115">Sélectionnez **obtenir** ou **installer** sur la page d’application (un achat peut être nécessaire).</span><span class="sxs-lookup"><span data-stu-id="599bb-115">Select **Get** or **Install** on the application's page (a purchase may be required).</span></span>

### <a name="installing-an-application-package-with-the-device-portal"></a><span data-ttu-id="599bb-116">L’installation d’un package d’application avec le portail de l’appareil</span><span class="sxs-lookup"><span data-stu-id="599bb-116">Installing an application package with the Device Portal</span></span>
1. <span data-ttu-id="599bb-117">Établir une connexion à partir de [appareil portail](using-the-windows-device-portal.md) à la cible HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-117">Establish a connection from [Device Portal](using-the-windows-device-portal.md) to the target HoloLens.</span></span>
2. <span data-ttu-id="599bb-118">Accédez à la **applications** page dans le volet de navigation gauche.</span><span class="sxs-lookup"><span data-stu-id="599bb-118">Navigate to the **Apps** page in the left navigation.</span></span>
3. <span data-ttu-id="599bb-119">Sous **Package d’application** accédez au fichier .aspx associé à votre application.</span><span class="sxs-lookup"><span data-stu-id="599bb-119">Under **App Package** Browse to the .appx file associated with your application.</span></span>
  >[!IMPORTANT]
  ><span data-ttu-id="599bb-120">Veillez à référencer les fichiers de dépendance et les certificats associés.</span><span class="sxs-lookup"><span data-stu-id="599bb-120">Make sure to reference any associated dependency and certificate files.</span></span>

4. <span data-ttu-id="599bb-121">Cliquez sur **accédez**.</span><span class="sxs-lookup"><span data-stu-id="599bb-121">Click **Go**.</span></span>

<span data-ttu-id="599bb-122">![Installer le formulaire d’application dans Windows Device Portal sur Microsoft HoloLens](images/deviceportal-appmanager.jpg)</span><span class="sxs-lookup"><span data-stu-id="599bb-122">![Install app form in Windows Device Portal on Microsoft HoloLens](images/deviceportal-appmanager.jpg)</span></span><br>
<span data-ttu-id="599bb-123">À l’aide de Windows Device Portal pour installer une application sur HoloLens</span><span class="sxs-lookup"><span data-stu-id="599bb-123">Using Windows Device Portal to install an app on HoloLens</span></span>

### <a name="deploying-from-microsoft-visual-studio-2015"></a><span data-ttu-id="599bb-124">Déploiement à partir de Microsoft Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="599bb-124">Deploying from Microsoft Visual Studio 2015</span></span>
1. <span data-ttu-id="599bb-125">Ouvrez la solution de Visual Studio de votre application (fichier .sln).</span><span class="sxs-lookup"><span data-stu-id="599bb-125">Open your app's Visual Studio solution (.sln file).</span></span>
2. <span data-ttu-id="599bb-126">Ouvrez le projet **propriétés** .</span><span class="sxs-lookup"><span data-stu-id="599bb-126">Open the project's **Properties** .</span></span>
3. <span data-ttu-id="599bb-127">Sélectionnez la configuration de build suivant : Ordinateur maître/x86/distant.</span><span class="sxs-lookup"><span data-stu-id="599bb-127">Select the following build configuration: Master/x86/Remote Machine.</span></span>
4. <span data-ttu-id="599bb-128">Lorsque vous sélectionnez la Machine distante :</span><span class="sxs-lookup"><span data-stu-id="599bb-128">When you select Remote Machine:</span></span>
   * <span data-ttu-id="599bb-129">Assurez-vous que les points d’adresse en adresse de WiFi IP des HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-129">Make sure the address points to the HoloLens' WiFi IP address.</span></span>
   * <span data-ttu-id="599bb-130">Définir l’authentification sur universel (protocole non chiffré).</span><span class="sxs-lookup"><span data-stu-id="599bb-130">Set authentication to Universal (Unencrypted Protocol).</span></span>
5. <span data-ttu-id="599bb-131">Générez votre solution.</span><span class="sxs-lookup"><span data-stu-id="599bb-131">Build your solution.</span></span>
6. <span data-ttu-id="599bb-132">Cliquez sur le **Machine distante** bouton pour déployer l’application à partir de votre PC de développement pour votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-132">Click the **Remote Machine** button to deploy the app from your development PC to your HoloLens.</span></span> <span data-ttu-id="599bb-133">Si vous avez déjà une build existante sur le HoloLens, sélectionnez Oui pour réinstaller cette version plus récente.</span><span class="sxs-lookup"><span data-stu-id="599bb-133">If you already have an existing build on the HoloLens, select yes to re-install this newer version.</span></span><br>
  <span data-ttu-id="599bb-134">![Déploiement de Machine à distance pour les applications pour Microsoft HoloLens dans Visual Studio](images/vs2015-remotedeployment.jpg)</span><span class="sxs-lookup"><span data-stu-id="599bb-134">![Remote Machine deployment for apps to Microsoft HoloLens in Visual Studio](images/vs2015-remotedeployment.jpg)</span></span><br>
7. <span data-ttu-id="599bb-135">L’application installera et auto lancement sur votre HoloLens.</span><span class="sxs-lookup"><span data-stu-id="599bb-135">The application will install and auto launch on your HoloLens.</span></span>
