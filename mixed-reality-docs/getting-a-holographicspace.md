---
title: Obtention d’un HolographicSpace
description: Explique l’API HolographicSpace, un concept fondamental pour le rendu holographique et entrée spatiale.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HolographicSpace, CoreWindow, spatiale d’entrée, de rendu, remplacez la chaîne, frame HOLOGRAPHIQUE, boucle de mise à jour, boucle du jeu, de référence, locatability, exemple de code, procédure pas à pas
ms.openlocfilehash: 828352203b20ec38275796b3f172e7ecc5df3f00
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597117"
---
# <a name="getting-a-holographicspace"></a><span data-ttu-id="41849-104">Obtention d’un HolographicSpace</span><span class="sxs-lookup"><span data-stu-id="41849-104">Getting a HolographicSpace</span></span>

<span data-ttu-id="41849-105">Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> classe est votre portail dans le monde HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-105">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class is your portal into the holographic world.</span></span> <span data-ttu-id="41849-106">Il contrôle rendu immersif, fournit des données de l’appareil photo et fournit l’accès aux API de raisonnement spatiale.</span><span class="sxs-lookup"><span data-stu-id="41849-106">It controls immersive rendering, provides camera data, and provides access to spatial reasoning APIs.</span></span> <span data-ttu-id="41849-107">Vous allez créer une pour votre application UWP <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> ou HWND de votre application Win32.</span><span class="sxs-lookup"><span data-stu-id="41849-107">You will create one for your UWP app's <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> or your Win32 app's HWND.</span></span>

## <a name="set-up-the-holographic-space"></a><span data-ttu-id="41849-108">Configurer l’espace HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="41849-108">Set up the holographic space</span></span>

<span data-ttu-id="41849-109">Création de l’objet espace holographique est la première étape dans votre application Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="41849-109">Creating the holographic space object is the first step in making your Windows Mixed Reality app.</span></span> <span data-ttu-id="41849-110">Les applications Windows traditionnelles restituent à une chaîne de permutation de Direct3D créée pour la fenêtre de base de leur vue de l’application.</span><span class="sxs-lookup"><span data-stu-id="41849-110">Traditional Windows apps render to a Direct3D swap chain created for the core window of their application view.</span></span> <span data-ttu-id="41849-111">Cette chaîne de permutation est affichée pour une ardoise dans l’interface utilisateur HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-111">This swap chain is displayed to a slate in the holographic UI.</span></span> <span data-ttu-id="41849-112">Pour rendre votre vue de l’application HOLOGRAPHIQUE au lieu d’une ardoise 2D, créer un espace HOLOGRAPHIQUE sa fenêtre core au lieu d’une chaîne de permutation.</span><span class="sxs-lookup"><span data-stu-id="41849-112">To make your application view holographic rather than a 2D slate, create a holographic space for its core window instead of a swap chain.</span></span> <span data-ttu-id="41849-113">Présentation HOLOGRAPHIQUE frames qui sont créés par cet espace HOLOGRAPHIQUE met votre application en mode de rendu de plein écran.</span><span class="sxs-lookup"><span data-stu-id="41849-113">Presenting holographic frames that are created by this holographic space puts your app into full-screen rendering mode.</span></span>

<span data-ttu-id="41849-114">Pour un **application UWP** [à partir de la *modèle d’application de 11 HOLOGRAPHIQUE DirectX (Windows universel)*](creating-a-holographic-directx-project.md), recherchez ce code dans le **SetWindow** méthode dans AppView.cpp :</span><span class="sxs-lookup"><span data-stu-id="41849-114">For a **UWP app** [starting from the *Holographic DirectX 11 App (Universal Windows) template*](creating-a-holographic-directx-project.md), look for this code in the **SetWindow** method in AppView.cpp:</span></span>

```cpp
m_holographicSpace = HolographicSpace::CreateForCoreWindow(window);
```

<span data-ttu-id="41849-115">Pour un **application Win32** [à partir de la *BasicHologram* Win32, exemple](creating-a-holographic-directx-project.md#creating-a-win32-project), examinez **App::CreateWindowAndHolographicSpace** pour un exemple montrant comment créer un HWND et le convertir en un HWND immersif en créant associé à un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>:</span><span class="sxs-lookup"><span data-stu-id="41849-115">For a **Win32 app** [starting from the *BasicHologram* Win32 sample](creating-a-holographic-directx-project.md#creating-a-win32-project), look at **App::CreateWindowAndHolographicSpace** for an example of how to create an HWND and then convert it into an immersive HWND by creating an associated <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>:</span></span>
```cpp
void App::CreateWindowAndHolographicSpace(HINSTANCE hInstance, int nCmdShow)
{
    // Store the instance handle in our class variable.
    m_hInst = hInstance;

    // Create the window for the HolographicSpace.
    hWnd = CreateWindowW(
        m_szWindowClass, 
        m_szTitle,
        WS_VISIBLE,
        CW_USEDEFAULT, 
        0, 
        CW_USEDEFAULT, 
        0, 
        nullptr, 
        nullptr, 
        hInstance, 
        nullptr);

    if (!hWnd)
    {
        winrt::check_hresult(E_FAIL);
    }

    {
        // Use WinRT factory to create the holographic space.
        using namespace winrt::Windows::Graphics::Holographic;
        winrt::com_ptr<IHolographicSpaceInterop> holographicSpaceInterop =
            winrt::get_activation_factory<HolographicSpace, IHolographicSpaceInterop>();
        winrt::com_ptr<ABI::Windows::Graphics::Holographic::IHolographicSpace> spHolographicSpace;
        winrt::check_hresult(holographicSpaceInterop->CreateForWindow(
            hWnd, __uuidof(ABI::Windows::Graphics::Holographic::IHolographicSpace),
            winrt::put_abi(spHolographicSpace)));

        if (!spHolographicSpace)
        {
            winrt::check_hresult(E_FAIL);
        }

        // Store the holographic space.
        m_holographicSpace = spHolographicSpace.as<HolographicSpace>();
    }

    // The DeviceResources class uses the preferred DXGI adapter ID from the holographic
    // space (when available) to create a Direct3D device. The HolographicSpace
    // uses this ID3D11Device to create and manage device-based resources such as
    // swap chains.
    m_deviceResources->SetHolographicSpace(m_holographicSpace);

    // The main class uses the holographic space for updates and rendering.
    m_main->SetHolographicSpace(hWnd, m_holographicSpace);

    // Show the window. This will activate the holographic view and switch focus
    // to the app in Windows Mixed Reality.
    ShowWindow(hWnd, nCmdShow);
    UpdateWindow(hWnd);
}
```

<span data-ttu-id="41849-116">Maintenant que vous avez obtenu un HolographicSpace pour votre UWP CoreWindow ou le HWND Win32, vous utiliserez ce HolographicSpace pour gérer les caméras HOLOGRAPHIQUE, créer des systèmes de coordonnées et effectuer le rendu HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-116">Now that you've obtained a HolographicSpace for either your UWP CoreWindow or Win32 HWND, you'll use that HolographicSpace to handle holographic cameras, create coordinate systems and do holographic rendering.</span></span> <span data-ttu-id="41849-117">L’espace HOLOGRAPHIQUE actuel est utilisé dans plusieurs endroits dans le modèle de DirectX :</span><span class="sxs-lookup"><span data-stu-id="41849-117">The current holographic space is used in multiple places in the DirectX template:</span></span>
* <span data-ttu-id="41849-118">Le **DeviceResources** classe a besoin d’obtenir des informations à partir de l’objet HolographicSpace afin de créer le périphérique Direct3D.</span><span class="sxs-lookup"><span data-stu-id="41849-118">The **DeviceResources** class needs to get some information from the HolographicSpace object in order to create the Direct3D device.</span></span> <span data-ttu-id="41849-119">Il s’agit de l’ID de carte DXGI associé à l’écran holographique.</span><span class="sxs-lookup"><span data-stu-id="41849-119">This is the DXGI adapter ID associated with the holographic display.</span></span> <span data-ttu-id="41849-120">Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> classe utilise un appareil de Direct3D 11 de votre application pour créer et gérer des ressources basées sur les appareils, tels que les mémoires tampons d’arrière-plan pour chaque caméra HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-120">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class uses your app's Direct3D 11 device to create and manage device-based resources, such as the back buffers for each holographic camera.</span></span> <span data-ttu-id="41849-121">Si vous voulez voir ce que fait cette fonction sous le capot, vous la trouverez dans DeviceResources.cpp.</span><span class="sxs-lookup"><span data-stu-id="41849-121">If you're interested in seeing what this function does under the hood, you'll find it in DeviceResources.cpp.</span></span>
* <span data-ttu-id="41849-122">La fonction **DeviceResources::InitializeUsingHolographicSpace** montre comment obtenir l’adaptateur en recherchant le LUID – et comment choisir un adaptateur par défaut lorsque aucune carte préférée n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="41849-122">The function **DeviceResources::InitializeUsingHolographicSpace** demonstrates how to obtain the adapter by looking up the LUID – and how to choose a default adapter when no preferred adapter is specified.</span></span>
* <span data-ttu-id="41849-123">Classe principale de l’application utilise l’espace holographique de **AppView::SetWindow** ou **App::CreateWindowAndHolographicSpace** pour les mises à jour et de rendu.</span><span class="sxs-lookup"><span data-stu-id="41849-123">The app's main class uses the holographic space from **AppView::SetWindow** or **App::CreateWindowAndHolographicSpace** for updates and rendering.</span></span>

>[!NOTE]
><span data-ttu-id="41849-124">Tandis que les sections ci-dessous mentionner les noms de fonction à partir du modèle comme **AppView::SetWindow** qui supposent que vous avez démarré à partir du modèle d’application UWP HOLOGRAPHIQUE, les extraits de code que vous voyez seront applique également dans les applications UWP et Win32.</span><span class="sxs-lookup"><span data-stu-id="41849-124">While the sections below mention function names from the template like **AppView::SetWindow** that assume that you started from the holographic UWP app template, the code snippets you see will apply equally across UWP and Win32 apps.</span></span>

<span data-ttu-id="41849-125">Ensuite, nous nous plongerons dans le programme d’installation qui traiter **SetHolographicSpace** est chargé dans la classe AppMain.</span><span class="sxs-lookup"><span data-stu-id="41849-125">Next, we'll dive into the setup process that **SetHolographicSpace** is responsible for in the AppMain class.</span></span>

## <a name="subscribe-to-camera-events-create-and-remove-camera-resources"></a><span data-ttu-id="41849-126">S’abonner aux événements de l’appareil photo, créer et supprimer des ressources de l’appareil photo</span><span class="sxs-lookup"><span data-stu-id="41849-126">Subscribe to camera events, create and remove camera resources</span></span>

<span data-ttu-id="41849-127">Contenu holographique de votre application se trouve dans son espace holographique et est affichée via un ou plusieurs caméras HOLOGRAPHIQUE qui représentent différentes perspectives sur la scène.</span><span class="sxs-lookup"><span data-stu-id="41849-127">Your app's holographic content lives in its holographic space, and is viewed through one or more holographic cameras which represent different perspectives on the scene.</span></span> <span data-ttu-id="41849-128">Maintenant que vous avez l’espace HOLOGRAPHIQUE, vous pouvez recevoir des données d’appareils photo HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-128">Now that you have the holographic space, you can receive data for holographic cameras.</span></span>

<span data-ttu-id="41849-129">Votre application doit répondre aux **CameraAdded** événements en créant toutes les ressources qui sont spécifiques à cet appareil photo, tels que votre mémoire tampon d’arrière-plan restituer la vue cible.</span><span class="sxs-lookup"><span data-stu-id="41849-129">Your app needs to respond to **CameraAdded** events by creating any resources that are specific to that camera, like your back buffer render target view.</span></span> <span data-ttu-id="41849-130">Vous pouvez voir ce code dans le **DeviceResources::SetHolographicSpace** fonction, appelée par **AppView::SetWindow** avant que l’application crée des frames HOLOGRAPHIQUE :</span><span class="sxs-lookup"><span data-stu-id="41849-130">You can see this code in the **DeviceResources::SetHolographicSpace** function, called by **AppView::SetWindow** before the app creates any holographic frames:</span></span>

```cpp
m_cameraAddedToken = m_holographicSpace.CameraAdded(
    std::bind(&AppMain::OnCameraAdded, this, _1, _2));
```

<span data-ttu-id="41849-131">Votre application doit également répondre aux **CameraRemoved** événements en libérant les ressources qui ont été créés pour cet appareil photo.</span><span class="sxs-lookup"><span data-stu-id="41849-131">Your app also needs to respond to **CameraRemoved** events by releasing resources that were created for that camera.</span></span>

<span data-ttu-id="41849-132">À partir de **DeviceResources::SetHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="41849-132">From **DeviceResources::SetHolographicSpace**:</span></span>

```cpp
m_cameraRemovedToken = m_holographicSpace.CameraRemoved(
    std::bind(&AppMain::OnCameraRemoved, this, _1, _2));
```

<span data-ttu-id="41849-133">Les gestionnaires d’événements doivent effectuer certaines tâches afin de conserver l’échange de données, de rendu holographique et afin que votre application est en mesure d’effectuer le rendu du tout.</span><span class="sxs-lookup"><span data-stu-id="41849-133">The event handlers must complete some work in order to keep holographic rendering flowing smoothly, and so that your app is able to render at all.</span></span> <span data-ttu-id="41849-134">Lire le code et les commentaires pour plus d’informations : vous pouvez rechercher des **OnCameraAdded** et **OnCameraRemoved** dans votre classe principale pour comprendre comment la **m_cameraResources** map est géré par **DeviceResources**.</span><span class="sxs-lookup"><span data-stu-id="41849-134">Read the code and comments for the details: you can look for **OnCameraAdded** and **OnCameraRemoved** in your main class to understand how the **m_cameraResources** map is handled by **DeviceResources**.</span></span>

<span data-ttu-id="41849-135">À ce stade, nous nous concentrons sur AppMain et le programme d’installation qu’il fait pour activer votre application pour connaître les caméras HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-135">Right now, we're focused on AppMain and the setup that it does to enable your app to know about holographic cameras.</span></span> <span data-ttu-id="41849-136">Dans cet esprit, il est important de tenir compte des deux conditions suivantes :</span><span class="sxs-lookup"><span data-stu-id="41849-136">With this in mind, it's important to take note of the following two requirements:</span></span>

1. <span data-ttu-id="41849-137">Pour le **CameraAdded** Gestionnaire d’événements, l’application peut fonctionner de façon asynchrone pour terminer la création de ressources et de chargement d’actifs pour le nouvel appareil photo HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="41849-137">For the **CameraAdded** event handler, the app can work asynchronously to finish creating resources and loading assets for the new holographic camera.</span></span> <span data-ttu-id="41849-138">Les applications qui prennent plusieurs frames pour effectuer ce travail doivent demander un report et terminer le report après le chargement asynchrone ; un [tâche PPL](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) peut être utilisé pour faire le travail asynchrone.</span><span class="sxs-lookup"><span data-stu-id="41849-138">Apps that take more than one frame to complete this work should request a deferral, and complete the deferral after loading asynchronously; a [PPL task](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) can be used to do asynchronous work.</span></span> <span data-ttu-id="41849-139">Votre application doit s’assurer qu’il est prêt pour le rendu à cet appareil photo immédiatement lorsqu’il termine le Gestionnaire d’événements, ou lorsqu’il s’achève le report.</span><span class="sxs-lookup"><span data-stu-id="41849-139">Your app must ensure that it's ready to render to that camera right away when it exits the event handler, or when it completes the deferral.</span></span> <span data-ttu-id="41849-140">Fermeture du Gestionnaire d’événements ou à la fin du report indique au système que votre application est maintenant prête à recevoir des trames holographique avec cette photo inclus.</span><span class="sxs-lookup"><span data-stu-id="41849-140">Exiting the event handler or completing the deferral tells the system that your app is now ready to receive holographic frames with that camera included.</span></span>

2. <span data-ttu-id="41849-141">Lorsque l’application reçoit un **CameraRemoved** événement, il doit libérer toutes les références à la mémoire tampon d’arrière-plan et la quitter immédiatement et la fonction.</span><span class="sxs-lookup"><span data-stu-id="41849-141">When the app receives a **CameraRemoved** event, it must release all references to the back buffer and exit the function right away.</span></span> <span data-ttu-id="41849-142">Cela inclut les vues de cible de rendu et toute autre ressource que peut contenir une référence à la [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource).</span><span class="sxs-lookup"><span data-stu-id="41849-142">This includes render target views, and any other resource that might hold a reference to the [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource).</span></span> <span data-ttu-id="41849-143">L’application doit également s’assurer que la mémoire tampon d’arrière-plan n’est pas attaché en tant que cible de rendu, comme indiqué dans **CameraResources::ReleaseResourcesForBackBuffer**.</span><span class="sxs-lookup"><span data-stu-id="41849-143">The app must also ensure that the back buffer is not attached as a render target, as shown in **CameraResources::ReleaseResourcesForBackBuffer**.</span></span> <span data-ttu-id="41849-144">Pour aider à accélérer le processus long, votre application peut libérer la mémoire tampon d’arrière-plan, puis lancer une tâche pour terminer de façon asynchrone n’importe quel autre travail n’est nécessaire de détruire ce appareil photo.</span><span class="sxs-lookup"><span data-stu-id="41849-144">To help speed things along, your app can release the back buffer and then launch a task to asynchronously complete any other work that is necessary to tear down that camera.</span></span> <span data-ttu-id="41849-145">Le modèle d’application HOLOGRAPHIQUE inclut une tâche PPL que vous pouvez utiliser à cet effet.</span><span class="sxs-lookup"><span data-stu-id="41849-145">The holographic app template includes a PPL task that you can use for this purpose.</span></span>

>[!NOTE]
><span data-ttu-id="41849-146">Si vous souhaitez déterminer quand une caméra ajoutée ou supprimée apparaît sur l’image, utilisez le **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) et [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) propriétés.</span><span class="sxs-lookup"><span data-stu-id="41849-146">If you want to determine when an added or removed camera shows up on the frame, use the **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) and [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) properties.</span></span>

## <a name="create-a-frame-of-reference-for-your-holographic-content"></a><span data-ttu-id="41849-147">Créer un cadre de référence pour votre contenu HOLOGRAPHIQUE</span><span class="sxs-lookup"><span data-stu-id="41849-147">Create a frame of reference for your holographic content</span></span>

<span data-ttu-id="41849-148">Contenu de votre application doit être positionné dans un [système de coordonnées spatial](coordinate-systems-in-directx.md) à restituer dans le HolographicSpace.</span><span class="sxs-lookup"><span data-stu-id="41849-148">Your app's content must be positioned in a [spatial coordinate system](coordinate-systems-in-directx.md) to be rendered in the HolographicSpace.</span></span> <span data-ttu-id="41849-149">Le système fournit deux principal de référence que vous pouvez utiliser pour établir un système de coordonnées pour votre hologrammes.</span><span class="sxs-lookup"><span data-stu-id="41849-149">The system provides two primary frames of reference which you can use to establish a coordinate system for your holograms.</span></span>

<span data-ttu-id="41849-150">Il existe deux sortes de trames de référence dans Windows HOLOGRAPHIQUE : référencer les images associées à l’appareil et les trames de référence restent STATIONNAIRES lorsque se trouve l’appareil via l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41849-150">There are two kinds of reference frames in Windows Holographic: reference frames attached to the device, and reference frames that remain stationary as the device moves through the user's environment.</span></span> <span data-ttu-id="41849-151">Le modèle d’application HOLOGRAPHIQUE utilise un cadre de référence stationnaire par défaut ; Il s’agit d’une des manières plus simples pour restituer hologrammes verrouillé de monde.</span><span class="sxs-lookup"><span data-stu-id="41849-151">The holographic app template uses a stationary reference frame by default; this is one of the simplest ways to render world-locked holograms.</span></span>

<span data-ttu-id="41849-152">Trames de référence stationnaire sont conçus pour stabiliser les positions proche de l’emplacement actuel de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="41849-152">Stationary reference frames are designed to stabilize positions near the device's current location.</span></span> <span data-ttu-id="41849-153">Cela signifie que les coordonnées plus éloigné de l’appareil sont autorisées à dérives légèrement en ce qui concerne l’environnement utilisateur, comme l’appareil en apprend plus sur l’espace autour de lui.</span><span class="sxs-lookup"><span data-stu-id="41849-153">This means that coordinates further from the device are allowed to drift slightly with respect to the user's environment as the device learns more about the space around it.</span></span> <span data-ttu-id="41849-154">Il existe deux façons de créer un système de référence stationnaire : acquérir le système de coordonnées à partir de la [étape spatial](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), ou utiliser la valeur par défaut <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span><span class="sxs-lookup"><span data-stu-id="41849-154">There are two ways to create a stationary frame of reference: acquire the coordinate system from the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), or use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span> <span data-ttu-id="41849-155">Si vous créez une application Windows Mixed Reality pour des casques IMMERSIFS, le point de départ recommandé est la [étape spatial](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), qui fournit également des informations sur les fonctionnalités du casque immersive porté par le lecteur.</span><span class="sxs-lookup"><span data-stu-id="41849-155">If you are creating a Windows Mixed Reality app for immersive headsets, the recommended starting point is the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), which also provides information about the capabilities of the immersive headset worn by the player.</span></span> <span data-ttu-id="41849-156">Ici, nous montrons comment utiliser la valeur par défaut <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span><span class="sxs-lookup"><span data-stu-id="41849-156">Here, we show how to use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span>

<span data-ttu-id="41849-157">Le localisateur spatial représente le périphérique Windows Mixed Reality et effectue le suivi du mouvement de l’appareil et fournit des systèmes de coordonnées qui peuvent être reconnus par rapport à son emplacement.</span><span class="sxs-lookup"><span data-stu-id="41849-157">The spatial locator represents the Windows Mixed Reality device, and tracks the motion of the device and provides coordinate systems that can be understood relative to its location.</span></span>

<span data-ttu-id="41849-158">À partir de **AppMain::OnHolographicDisplayIsAvailableChanged**:</span><span class="sxs-lookup"><span data-stu-id="41849-158">From **AppMain::OnHolographicDisplayIsAvailableChanged**:</span></span>

```cpp
spatialLocator = SpatialLocator::GetDefault();
```

<span data-ttu-id="41849-159">Créer une fois l’image de référence stationnaire lorsque l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="41849-159">Create the stationary reference frame once when the app is launched.</span></span> <span data-ttu-id="41849-160">Ceci est analogue à la définition d’un système de coordonnées de monde, avec l’origine placé à la position de l’appareil lorsque l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="41849-160">This is analogous to defining a world coordinate system, with the origin placed at the device's position when the app is launched.</span></span> <span data-ttu-id="41849-161">Cette image de référence ne déplace pas avec l’appareil.</span><span class="sxs-lookup"><span data-stu-id="41849-161">This reference frame doesn't move with the device.</span></span>

<span data-ttu-id="41849-162">À partir de **AppMain::SetHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="41849-162">From **AppMain::SetHolographicSpace**:</span></span>

```cpp
m_stationaryReferenceFrame =
    m_spatialLocator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```

<span data-ttu-id="41849-163">Toutes les trames de référence sont gravité aligné, cela signifie que l’axe des y pointe « up » en ce qui concerne l’environnement utilisateur.</span><span class="sxs-lookup"><span data-stu-id="41849-163">All reference frames are gravity aligned, meaning that the y axis points "up" with respect to the user's environment.</span></span> <span data-ttu-id="41849-164">Étant donné que Windows utilise les systèmes de coordonnées « droitiers », la direction de l’axe z – coïncide avec la direction « forward », que l’appareil est face lors de la création de l’image de référence.</span><span class="sxs-lookup"><span data-stu-id="41849-164">Since Windows uses "right-handed" coordinate systems, the direction of the –z axis coincides with the "forward" direction the device is facing when the reference frame is created.</span></span>

>[!NOTE]
><span data-ttu-id="41849-165">Lorsque votre application requiert le positionnement précis des hologrammes individuels, utilisez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> pour ancrer l’hologramme individuel vers une position dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="41849-165">When your app requires precise placement of individual holograms, use a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> to anchor the individual hologram to a position in the real world.</span></span> <span data-ttu-id="41849-166">Par exemple, utiliser un point d’ancrage spatial lorsque l’utilisateur indique un point de présenter un intérêt particulier.</span><span class="sxs-lookup"><span data-stu-id="41849-166">For example, use a spatial anchor when the user indicates a point to be of special interest.</span></span> <span data-ttu-id="41849-167">Les positions d’ancrage ne pas dérive, mais ils peuvent être ajustés.</span><span class="sxs-lookup"><span data-stu-id="41849-167">Anchor positions do not drift, but they can be adjusted.</span></span> <span data-ttu-id="41849-168">Par défaut, lorsqu’un point d’ancrage est ajustée, ce qui facilite sa position en place sur les images de plusieurs suivants après la correction.</span><span class="sxs-lookup"><span data-stu-id="41849-168">By default, when an anchor is adjusted, it eases its position into place over the next several frames after the correction has occurred.</span></span> <span data-ttu-id="41849-169">En fonction de votre application, dans ce cas vous souhaiterez traiter l’ajustement d’une manière différente (par exemple en différer jusqu'à ce que l’hologramme n’est pas visible).</span><span class="sxs-lookup"><span data-stu-id="41849-169">Depending on your application, when this occurs you may want to handle the adjustment in a different manner (e.g. by deferring it until the hologram is out of view).</span></span> <span data-ttu-id="41849-170">Le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> propriété et <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> événements activer ces personnalisations.</span><span class="sxs-lookup"><span data-stu-id="41849-170">The <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> property and <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> events enable these customizations.</span></span>

## <a name="respond-to-locatability-changed-events"></a><span data-ttu-id="41849-171">Répondre aux événements de locatability modifié</span><span class="sxs-lookup"><span data-stu-id="41849-171">Respond to locatability changed events</span></span>

<span data-ttu-id="41849-172">Rendu hologrammes verrouillé de monde nécessite l’appareil soit en mesure de localiser lui-même dans le monde.</span><span class="sxs-lookup"><span data-stu-id="41849-172">Rendering world-locked holograms requires the device to be able to locate itself in the world.</span></span> <span data-ttu-id="41849-173">Cela n'est pas toujours possible en raison de conditions environnementales, et si tel est le cas, l’utilisateur peut attendre une indication visuelle de l’interruption de suivi.</span><span class="sxs-lookup"><span data-stu-id="41849-173">This may not always be possible due to environmental conditions, and if so, the user may expect a visual indication of the tracking interruption.</span></span> <span data-ttu-id="41849-174">Cette indication visuelle doit être restituée à l’aide d’images de référence associées à l’appareil, au lieu d’arrêt au monde.</span><span class="sxs-lookup"><span data-stu-id="41849-174">This visual indication must be rendered using reference frames attached to the device, instead of stationary to the world.</span></span>

<span data-ttu-id="41849-175">Votre application peut demander à être averti si le suivi est interrompu pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="41849-175">You app can request to be notified if tracking is interrupted for any reason.</span></span> <span data-ttu-id="41849-176">S’inscrire pour l’événement LocatabilityChanged détecter lorsque la capacité du périphérique à s’y localiser les modifications du monde.</span><span class="sxs-lookup"><span data-stu-id="41849-176">Register for the LocatabilityChanged event to detect when the device's ability to locate itself in the world changes.</span></span> <span data-ttu-id="41849-177">À partir de **AppMain::SetHolographicSpace :**</span><span class="sxs-lookup"><span data-stu-id="41849-177">From **AppMain::SetHolographicSpace:**</span></span>

```cpp
m_locatabilityChangedToken = m_spatialLocator.LocatabilityChanged(
    std::bind(&HolographicApp6Main::OnLocatabilityChanged, this, _1, _2));
```

<span data-ttu-id="41849-178">Ensuite, utilisez cet événement pour déterminer quand hologrammes ne peut pas être restitués STATIONNAIRES au monde.</span><span class="sxs-lookup"><span data-stu-id="41849-178">Then use this event to determine when holograms cannot be rendered stationary to the world.</span></span>

## <a name="see-also"></a><span data-ttu-id="41849-179">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="41849-179">See also</span></span>
* [<span data-ttu-id="41849-180">Rendu dans DirectX</span><span class="sxs-lookup"><span data-stu-id="41849-180">Rendering in DirectX</span></span>](rendering-in-directx.md)
* [<span data-ttu-id="41849-181">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="41849-181">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
