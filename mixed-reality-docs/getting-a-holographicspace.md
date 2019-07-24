---
title: Obtention d’un HolographicSpace
description: Explique l’API HolographicSpace, un concept fondamental pour le rendu holographique et l’entrée spatiale.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, HolographicSpace, CoreWindow, entrée spatiale, rendu, chaîne de permutation, Frame holographique, boucle de mise à jour, boucle de jeu, frame de référence, localisation, exemple de code, procédure pas à pas
ms.openlocfilehash: 828352203b20ec38275796b3f172e7ecc5df3f00
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63525449"
---
# <a name="getting-a-holographicspace"></a><span data-ttu-id="b8f03-104">Obtention d’un HolographicSpace</span><span class="sxs-lookup"><span data-stu-id="b8f03-104">Getting a HolographicSpace</span></span>

<span data-ttu-id="b8f03-105">La classe <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> est votre portail dans le monde holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-105">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class is your portal into the holographic world.</span></span> <span data-ttu-id="b8f03-106">Il contrôle le rendu immersif, fournit des données d’appareil photo et donne accès aux API de raisonnement spatial.</span><span class="sxs-lookup"><span data-stu-id="b8f03-106">It controls immersive rendering, provides camera data, and provides access to spatial reasoning APIs.</span></span> <span data-ttu-id="b8f03-107">Vous allez en créer un pour le <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> de votre application UWP ou le HWND de votre application Win32.</span><span class="sxs-lookup"><span data-stu-id="b8f03-107">You will create one for your UWP app's <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> or your Win32 app's HWND.</span></span>

## <a name="set-up-the-holographic-space"></a><span data-ttu-id="b8f03-108">Configurer l’espace holographique</span><span class="sxs-lookup"><span data-stu-id="b8f03-108">Set up the holographic space</span></span>

<span data-ttu-id="b8f03-109">La création de l’objet espace holographique est la première étape de la création de votre application Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="b8f03-109">Creating the holographic space object is the first step in making your Windows Mixed Reality app.</span></span> <span data-ttu-id="b8f03-110">Les applications Windows traditionnelles sont rendues dans une chaîne de permutation Direct3D créée pour la fenêtre principale de leur vue d’application.</span><span class="sxs-lookup"><span data-stu-id="b8f03-110">Traditional Windows apps render to a Direct3D swap chain created for the core window of their application view.</span></span> <span data-ttu-id="b8f03-111">Cette chaîne de permutation s’affiche dans une ardoise dans l’interface utilisateur holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-111">This swap chain is displayed to a slate in the holographic UI.</span></span> <span data-ttu-id="b8f03-112">Pour que votre application affiche holographique plutôt qu’une ardoise 2D, créez un espace holographique pour sa fenêtre principale au lieu d’une chaîne de permutation.</span><span class="sxs-lookup"><span data-stu-id="b8f03-112">To make your application view holographic rather than a 2D slate, create a holographic space for its core window instead of a swap chain.</span></span> <span data-ttu-id="b8f03-113">La présentation des frames holographiques créés par cet espace holographique place votre application en mode de rendu plein écran.</span><span class="sxs-lookup"><span data-stu-id="b8f03-113">Presenting holographic frames that are created by this holographic space puts your app into full-screen rendering mode.</span></span>

<span data-ttu-id="b8f03-114">Pour une **application UWP** à [partir du *modèle d’application holographique DirectX 11 (Windows universel)* ](creating-a-holographic-directx-project.md), recherchez ce code dans la méthode **SetWindow** dans AppView. cpp:</span><span class="sxs-lookup"><span data-stu-id="b8f03-114">For a **UWP app** [starting from the *Holographic DirectX 11 App (Universal Windows) template*](creating-a-holographic-directx-project.md), look for this code in the **SetWindow** method in AppView.cpp:</span></span>

```cpp
m_holographicSpace = HolographicSpace::CreateForCoreWindow(window);
```

<span data-ttu-id="b8f03-115">Pour une **application Win32** à [partir de l’exemple Win32 *BasicHologram* ](creating-a-holographic-directx-project.md#creating-a-win32-project), examinez **App:: CreateWindowAndHolographicSpace** pour obtenir un exemple de création d’un HWND, puis convertissez-le en un HWND immersif en créant un associé <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank"> HolographicSpace</a>:</span><span class="sxs-lookup"><span data-stu-id="b8f03-115">For a **Win32 app** [starting from the *BasicHologram* Win32 sample](creating-a-holographic-directx-project.md#creating-a-win32-project), look at **App::CreateWindowAndHolographicSpace** for an example of how to create an HWND and then convert it into an immersive HWND by creating an associated <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>:</span></span>
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

<span data-ttu-id="b8f03-116">Maintenant que vous avez obtenu un HolographicSpace pour votre CoreWindow UWP ou Win32 HWND, vous utiliserez ce HolographicSpace pour gérer les caméras holographiques, créer des systèmes de coordonnées et effectuer un rendu holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-116">Now that you've obtained a HolographicSpace for either your UWP CoreWindow or Win32 HWND, you'll use that HolographicSpace to handle holographic cameras, create coordinate systems and do holographic rendering.</span></span> <span data-ttu-id="b8f03-117">L’espace holographique actuel est utilisé à plusieurs endroits dans le modèle DirectX:</span><span class="sxs-lookup"><span data-stu-id="b8f03-117">The current holographic space is used in multiple places in the DirectX template:</span></span>
* <span data-ttu-id="b8f03-118">La classe **DeviceResources** doit recevoir des informations de l’objet HolographicSpace afin de créer l’appareil Direct3D.</span><span class="sxs-lookup"><span data-stu-id="b8f03-118">The **DeviceResources** class needs to get some information from the HolographicSpace object in order to create the Direct3D device.</span></span> <span data-ttu-id="b8f03-119">Il s’agit de l’ID d’adaptateur DXGI associé à l’affichage holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-119">This is the DXGI adapter ID associated with the holographic display.</span></span> <span data-ttu-id="b8f03-120">La classe <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> utilise le périphérique Direct3D 11 de votre application pour créer et gérer des ressources basées sur les appareils, telles que les mémoires tampons d’arrière-plan pour chaque caméra holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-120">The <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> class uses your app's Direct3D 11 device to create and manage device-based resources, such as the back buffers for each holographic camera.</span></span> <span data-ttu-id="b8f03-121">Si vous souhaitez voir ce que fait cette fonction sous le capot, vous le trouverez dans DeviceResources. cpp.</span><span class="sxs-lookup"><span data-stu-id="b8f03-121">If you're interested in seeing what this function does under the hood, you'll find it in DeviceResources.cpp.</span></span>
* <span data-ttu-id="b8f03-122">La fonction **DeviceResources:: InitializeUsingHolographicSpace** montre comment obtenir l’adaptateur en recherchant le LUID, et comment choisir un adaptateur par défaut quand aucun adaptateur préféré n’est spécifié.</span><span class="sxs-lookup"><span data-stu-id="b8f03-122">The function **DeviceResources::InitializeUsingHolographicSpace** demonstrates how to obtain the adapter by looking up the LUID – and how to choose a default adapter when no preferred adapter is specified.</span></span>
* <span data-ttu-id="b8f03-123">La classe principale de l’application utilise l’espace holographique de **AppView:: SetWindow** ou **App:: CreateWindowAndHolographicSpace** pour les mises à jour et le rendu.</span><span class="sxs-lookup"><span data-stu-id="b8f03-123">The app's main class uses the holographic space from **AppView::SetWindow** or **App::CreateWindowAndHolographicSpace** for updates and rendering.</span></span>

>[!NOTE]
><span data-ttu-id="b8f03-124">Tandis que les sections ci-dessous mentionnent les noms des fonctions du modèle comme **AppView:: SetWindow** , qui supposent que vous avez démarré à partir du modèle d’application UWP holographique, les extraits de code que vous voyez s’appliqueront également sur les applications UWP et Win32.</span><span class="sxs-lookup"><span data-stu-id="b8f03-124">While the sections below mention function names from the template like **AppView::SetWindow** that assume that you started from the holographic UWP app template, the code snippets you see will apply equally across UWP and Win32 apps.</span></span>

<span data-ttu-id="b8f03-125">Nous allons ensuite étudier le processus d’installation dont **SetHolographicSpace** est responsable dans la classe AppMain.</span><span class="sxs-lookup"><span data-stu-id="b8f03-125">Next, we'll dive into the setup process that **SetHolographicSpace** is responsible for in the AppMain class.</span></span>

## <a name="subscribe-to-camera-events-create-and-remove-camera-resources"></a><span data-ttu-id="b8f03-126">S’abonner aux événements de l’appareil photo, créer et supprimer des ressources d’appareil photo</span><span class="sxs-lookup"><span data-stu-id="b8f03-126">Subscribe to camera events, create and remove camera resources</span></span>

<span data-ttu-id="b8f03-127">Le contenu holographique de votre application réside dans son espace holographique et est affiché par le biais d’une ou de plusieurs caméras holographiques qui représentent différentes perspectives sur la scène.</span><span class="sxs-lookup"><span data-stu-id="b8f03-127">Your app's holographic content lives in its holographic space, and is viewed through one or more holographic cameras which represent different perspectives on the scene.</span></span> <span data-ttu-id="b8f03-128">Maintenant que vous disposez de l’espace holographique, vous pouvez recevoir des données pour les caméras holographiques.</span><span class="sxs-lookup"><span data-stu-id="b8f03-128">Now that you have the holographic space, you can receive data for holographic cameras.</span></span>

<span data-ttu-id="b8f03-129">Votre application doit répondre aux événements **CameraAdded** en créant toutes les ressources qui sont spécifiques à cette caméra, telles que la vue de la cible de rendu de la mémoire tampon d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="b8f03-129">Your app needs to respond to **CameraAdded** events by creating any resources that are specific to that camera, like your back buffer render target view.</span></span> <span data-ttu-id="b8f03-130">Vous pouvez voir ce code dans la fonction **DeviceResources:: SetHolographicSpace** , appelée par **AppView:: SetWindow** avant que l’application crée des frames holographiques:</span><span class="sxs-lookup"><span data-stu-id="b8f03-130">You can see this code in the **DeviceResources::SetHolographicSpace** function, called by **AppView::SetWindow** before the app creates any holographic frames:</span></span>

```cpp
m_cameraAddedToken = m_holographicSpace.CameraAdded(
    std::bind(&AppMain::OnCameraAdded, this, _1, _2));
```

<span data-ttu-id="b8f03-131">Votre application doit également répondre aux événements **CameraRemoved** en libérant les ressources qui ont été créées pour cette caméra.</span><span class="sxs-lookup"><span data-stu-id="b8f03-131">Your app also needs to respond to **CameraRemoved** events by releasing resources that were created for that camera.</span></span>

<span data-ttu-id="b8f03-132">À partir de **DeviceResources:: SetHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="b8f03-132">From **DeviceResources::SetHolographicSpace**:</span></span>

```cpp
m_cameraRemovedToken = m_holographicSpace.CameraRemoved(
    std::bind(&AppMain::OnCameraRemoved, this, _1, _2));
```

<span data-ttu-id="b8f03-133">Les gestionnaires d’événements doivent effectuer un travail afin de garantir le bon déroulement du rendu holographique et de permettre à votre application de s’afficher.</span><span class="sxs-lookup"><span data-stu-id="b8f03-133">The event handlers must complete some work in order to keep holographic rendering flowing smoothly, and so that your app is able to render at all.</span></span> <span data-ttu-id="b8f03-134">Pour plus d’informations, lisez le code et les commentaires suivants: vous pouvez rechercher **OnCameraAdded** et **OnCameraRemoved** dans votre classe principale pour comprendre comment la carte de **M_cameraResources** est gérée par **DeviceResources**.</span><span class="sxs-lookup"><span data-stu-id="b8f03-134">Read the code and comments for the details: you can look for **OnCameraAdded** and **OnCameraRemoved** in your main class to understand how the **m_cameraResources** map is handled by **DeviceResources**.</span></span>

<span data-ttu-id="b8f03-135">Pour le moment, nous nous concentrons sur AppMain et la configuration qu’il fait pour permettre à votre application de connaître les caméras holographiques.</span><span class="sxs-lookup"><span data-stu-id="b8f03-135">Right now, we're focused on AppMain and the setup that it does to enable your app to know about holographic cameras.</span></span> <span data-ttu-id="b8f03-136">Dans ce souci, il est important de prendre note des deux conditions suivantes:</span><span class="sxs-lookup"><span data-stu-id="b8f03-136">With this in mind, it's important to take note of the following two requirements:</span></span>

1. <span data-ttu-id="b8f03-137">Pour le gestionnaire d’événements **CameraAdded** , l’application peut fonctionner de manière asynchrone pour terminer la création de ressources et le chargement de ressources pour la nouvelle caméra holographique.</span><span class="sxs-lookup"><span data-stu-id="b8f03-137">For the **CameraAdded** event handler, the app can work asynchronously to finish creating resources and loading assets for the new holographic camera.</span></span> <span data-ttu-id="b8f03-138">Les applications qui prennent plus d’un cadre pour effectuer ce travail doivent demander un report et terminer le report après le chargement asynchrone. une [tâche ppl](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) peut être utilisée pour effectuer un travail asynchrone.</span><span class="sxs-lookup"><span data-stu-id="b8f03-138">Apps that take more than one frame to complete this work should request a deferral, and complete the deferral after loading asynchronously; a [PPL task](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) can be used to do asynchronous work.</span></span> <span data-ttu-id="b8f03-139">Votre application doit s’assurer qu’elle est prête à être rendue sur cette caméra immédiatement lorsqu’elle quitte le gestionnaire d’événements, ou lorsqu’elle termine le report.</span><span class="sxs-lookup"><span data-stu-id="b8f03-139">Your app must ensure that it's ready to render to that camera right away when it exits the event handler, or when it completes the deferral.</span></span> <span data-ttu-id="b8f03-140">Le fait de quitter le gestionnaire d’événements ou de terminer le report indique au système que votre application est maintenant prête à recevoir les images holographiques incluses dans cette caméra.</span><span class="sxs-lookup"><span data-stu-id="b8f03-140">Exiting the event handler or completing the deferral tells the system that your app is now ready to receive holographic frames with that camera included.</span></span>

2. <span data-ttu-id="b8f03-141">Lorsque l’application reçoit un événement **CameraRemoved** , elle doit libérer toutes les références à la mémoire tampon d’arrière-plan et quitter immédiatement la fonction.</span><span class="sxs-lookup"><span data-stu-id="b8f03-141">When the app receives a **CameraRemoved** event, it must release all references to the back buffer and exit the function right away.</span></span> <span data-ttu-id="b8f03-142">Cela comprend les affichages de cible de rendu et toute autre ressource qui peut contenir une référence à [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource).</span><span class="sxs-lookup"><span data-stu-id="b8f03-142">This includes render target views, and any other resource that might hold a reference to the [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource).</span></span> <span data-ttu-id="b8f03-143">L’application doit également s’assurer que la mémoire tampon d’arrière-plan n’est pas jointe en tant que cible de rendu, comme indiqué dans **CameraResources:: ReleaseResourcesForBackBuffer**.</span><span class="sxs-lookup"><span data-stu-id="b8f03-143">The app must also ensure that the back buffer is not attached as a render target, as shown in **CameraResources::ReleaseResourcesForBackBuffer**.</span></span> <span data-ttu-id="b8f03-144">Pour accélérer les choses, votre application peut libérer la mémoire tampon d’arrière-plan, puis lancer une tâche pour effectuer de façon asynchrone tout autre travail nécessaire pour détruire cette caméra.</span><span class="sxs-lookup"><span data-stu-id="b8f03-144">To help speed things along, your app can release the back buffer and then launch a task to asynchronously complete any other work that is necessary to tear down that camera.</span></span> <span data-ttu-id="b8f03-145">Le modèle d’application holographique comprend une tâche PPL que vous pouvez utiliser à cet effet.</span><span class="sxs-lookup"><span data-stu-id="b8f03-145">The holographic app template includes a PPL task that you can use for this purpose.</span></span>

>[!NOTE]
><span data-ttu-id="b8f03-146">Si vous souhaitez déterminer à quel moment une caméra ajoutée ou supprimée s’affiche sur le frame, utilisez les propriétés **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) et [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) .</span><span class="sxs-lookup"><span data-stu-id="b8f03-146">If you want to determine when an added or removed camera shows up on the frame, use the **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) and [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) properties.</span></span>

## <a name="create-a-frame-of-reference-for-your-holographic-content"></a><span data-ttu-id="b8f03-147">Créer un cadre de référence pour votre contenu holographique</span><span class="sxs-lookup"><span data-stu-id="b8f03-147">Create a frame of reference for your holographic content</span></span>

<span data-ttu-id="b8f03-148">Le contenu de votre application doit être positionné dans un [système de coordonnées spatiales](coordinate-systems-in-directx.md) pour être rendu dans le HolographicSpace.</span><span class="sxs-lookup"><span data-stu-id="b8f03-148">Your app's content must be positioned in a [spatial coordinate system](coordinate-systems-in-directx.md) to be rendered in the HolographicSpace.</span></span> <span data-ttu-id="b8f03-149">Le système fournit deux principales trames de référence que vous pouvez utiliser pour établir un système de coordonnées pour vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="b8f03-149">The system provides two primary frames of reference which you can use to establish a coordinate system for your holograms.</span></span>

<span data-ttu-id="b8f03-150">Il existe deux types de frames de référence dans Windows holographique: les frames de référence attachés à l’appareil et les trames de référence qui restent stationnaires lorsque l’appareil passe dans l’environnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f03-150">There are two kinds of reference frames in Windows Holographic: reference frames attached to the device, and reference frames that remain stationary as the device moves through the user's environment.</span></span> <span data-ttu-id="b8f03-151">Le modèle d’application holographique utilise un frame de référence fixe par défaut; Il s’agit de l’une des méthodes les plus simples pour restituer des hologrammes universels.</span><span class="sxs-lookup"><span data-stu-id="b8f03-151">The holographic app template uses a stationary reference frame by default; this is one of the simplest ways to render world-locked holograms.</span></span>

<span data-ttu-id="b8f03-152">Les images de référence fixes sont conçues pour stabiliser les positions près de l’emplacement actuel de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b8f03-152">Stationary reference frames are designed to stabilize positions near the device's current location.</span></span> <span data-ttu-id="b8f03-153">Cela signifie que les coordonnées du périphérique peuvent être légèrement déplacées par rapport à l’environnement de l’utilisateur, car ce dernier en apprend davantage sur l’espace qui l’entoure.</span><span class="sxs-lookup"><span data-stu-id="b8f03-153">This means that coordinates further from the device are allowed to drift slightly with respect to the user's environment as the device learns more about the space around it.</span></span> <span data-ttu-id="b8f03-154">Il existe deux façons de créer une image de référence stationnaire: acquérir le système de coordonnées à partir de la [Phase spatiale](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage)ou utilisez le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>par défaut.</span><span class="sxs-lookup"><span data-stu-id="b8f03-154">There are two ways to create a stationary frame of reference: acquire the coordinate system from the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), or use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span> <span data-ttu-id="b8f03-155">Si vous créez une application Windows Mixed Reality pour des casques immersifs, le point de départ recommandé est la [Phase spatiale](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), qui fournit également des informations sur les fonctionnalités du casque immersif porté par le joueur.</span><span class="sxs-lookup"><span data-stu-id="b8f03-155">If you are creating a Windows Mixed Reality app for immersive headsets, the recommended starting point is the [spatial stage](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), which also provides information about the capabilities of the immersive headset worn by the player.</span></span> <span data-ttu-id="b8f03-156">Ici, nous montrons comment utiliser le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>par défaut.</span><span class="sxs-lookup"><span data-stu-id="b8f03-156">Here, we show how to use the default <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.</span></span>

<span data-ttu-id="b8f03-157">Le localisateur spatial représente le périphérique Windows Mixed Reality et suit le mouvement de l’appareil et fournit des systèmes de coordonnées qui peuvent être compris par rapport à son emplacement.</span><span class="sxs-lookup"><span data-stu-id="b8f03-157">The spatial locator represents the Windows Mixed Reality device, and tracks the motion of the device and provides coordinate systems that can be understood relative to its location.</span></span>

<span data-ttu-id="b8f03-158">À partir de **AppMain:: OnHolographicDisplayIsAvailableChanged**:</span><span class="sxs-lookup"><span data-stu-id="b8f03-158">From **AppMain::OnHolographicDisplayIsAvailableChanged**:</span></span>

```cpp
spatialLocator = SpatialLocator::GetDefault();
```

<span data-ttu-id="b8f03-159">Créez le frame de référence fixe une fois l’application lancée.</span><span class="sxs-lookup"><span data-stu-id="b8f03-159">Create the stationary reference frame once when the app is launched.</span></span> <span data-ttu-id="b8f03-160">Cela équivaut à définir un système de coordonnées universelles, avec l’origine placée à la position de l’appareil lorsque l’application est lancée.</span><span class="sxs-lookup"><span data-stu-id="b8f03-160">This is analogous to defining a world coordinate system, with the origin placed at the device's position when the app is launched.</span></span> <span data-ttu-id="b8f03-161">Ce frame de référence ne se déplace pas avec l’appareil.</span><span class="sxs-lookup"><span data-stu-id="b8f03-161">This reference frame doesn't move with the device.</span></span>

<span data-ttu-id="b8f03-162">À partir de **AppMain:: SetHolographicSpace**:</span><span class="sxs-lookup"><span data-stu-id="b8f03-162">From **AppMain::SetHolographicSpace**:</span></span>

```cpp
m_stationaryReferenceFrame =
    m_spatialLocator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```

<span data-ttu-id="b8f03-163">Tous les frames de référence sont alignés par gravité, ce qui signifie que l’axe y pointe vers le haut par rapport à l’environnement de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b8f03-163">All reference frames are gravity aligned, meaning that the y axis points "up" with respect to the user's environment.</span></span> <span data-ttu-id="b8f03-164">Étant donné que Windows utilise des systèmes de coordonnées «droitiers», la direction de l’axe-z coïncide avec la direction «avant» à laquelle l’appareil est dirigé lorsque le frame de référence est créé.</span><span class="sxs-lookup"><span data-stu-id="b8f03-164">Since Windows uses "right-handed" coordinate systems, the direction of the –z axis coincides with the "forward" direction the device is facing when the reference frame is created.</span></span>

>[!NOTE]
><span data-ttu-id="b8f03-165">Lorsque votre application nécessite un positionnement précis des hologrammes individuels, utilisez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> pour ancrer l’hologramme individuel à une position dans le monde réel.</span><span class="sxs-lookup"><span data-stu-id="b8f03-165">When your app requires precise placement of individual holograms, use a <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> to anchor the individual hologram to a position in the real world.</span></span> <span data-ttu-id="b8f03-166">Par exemple, utilisez une ancre spatiale lorsque l’utilisateur indique un point qui présente un intérêt particulier.</span><span class="sxs-lookup"><span data-stu-id="b8f03-166">For example, use a spatial anchor when the user indicates a point to be of special interest.</span></span> <span data-ttu-id="b8f03-167">Les positions d’ancrage ne dérivent pas, mais elles peuvent être ajustées.</span><span class="sxs-lookup"><span data-stu-id="b8f03-167">Anchor positions do not drift, but they can be adjusted.</span></span> <span data-ttu-id="b8f03-168">Par défaut, lorsqu’un point d’ancrage est ajusté, il facilite sa position sur les différentes images après la correction.</span><span class="sxs-lookup"><span data-stu-id="b8f03-168">By default, when an anchor is adjusted, it eases its position into place over the next several frames after the correction has occurred.</span></span> <span data-ttu-id="b8f03-169">Selon votre application, lorsque cela se produit, vous souhaiterez peut-être gérer la modification d’une manière différente (par exemple, en la différant jusqu’à ce que l’hologramme soit hors de l’affichage).</span><span class="sxs-lookup"><span data-stu-id="b8f03-169">Depending on your application, when this occurs you may want to handle the adjustment in a different manner (e.g. by deferring it until the hologram is out of view).</span></span> <span data-ttu-id="b8f03-170">La propriété <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> et les événements <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> activent ces personnalisations.</span><span class="sxs-lookup"><span data-stu-id="b8f03-170">The <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> property and <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> events enable these customizations.</span></span>

## <a name="respond-to-locatability-changed-events"></a><span data-ttu-id="b8f03-171">Répondre aux événements de modification de la localisation</span><span class="sxs-lookup"><span data-stu-id="b8f03-171">Respond to locatability changed events</span></span>

<span data-ttu-id="b8f03-172">Le rendu des hologrammes dans le monde entier nécessite que l’appareil soit en mesure de se localiser dans le monde.</span><span class="sxs-lookup"><span data-stu-id="b8f03-172">Rendering world-locked holograms requires the device to be able to locate itself in the world.</span></span> <span data-ttu-id="b8f03-173">Cela n’est peut-être pas toujours possible en raison des conditions environnementales et, si tel est le cas, l’utilisateur peut s’attendre à une indication visuelle de l’interruption de suivi.</span><span class="sxs-lookup"><span data-stu-id="b8f03-173">This may not always be possible due to environmental conditions, and if so, the user may expect a visual indication of the tracking interruption.</span></span> <span data-ttu-id="b8f03-174">Cette indication visuelle doit être rendue à l’aide de frames de référence attachés à l’appareil, plutôt que stationnaire au monde.</span><span class="sxs-lookup"><span data-stu-id="b8f03-174">This visual indication must be rendered using reference frames attached to the device, instead of stationary to the world.</span></span>

<span data-ttu-id="b8f03-175">Vous pouvez demander à être averti si le suivi est interrompu pour une raison quelconque.</span><span class="sxs-lookup"><span data-stu-id="b8f03-175">You app can request to be notified if tracking is interrupted for any reason.</span></span> <span data-ttu-id="b8f03-176">Inscrivez-vous à l’événement LocatabilityChanged pour détecter le moment où la capacité de l’appareil à se trouver dans le monde change.</span><span class="sxs-lookup"><span data-stu-id="b8f03-176">Register for the LocatabilityChanged event to detect when the device's ability to locate itself in the world changes.</span></span> <span data-ttu-id="b8f03-177">À partir de **AppMain:: SetHolographicSpace:**</span><span class="sxs-lookup"><span data-stu-id="b8f03-177">From **AppMain::SetHolographicSpace:**</span></span>

```cpp
m_locatabilityChangedToken = m_spatialLocator.LocatabilityChanged(
    std::bind(&HolographicApp6Main::OnLocatabilityChanged, this, _1, _2));
```

<span data-ttu-id="b8f03-178">Utilisez ensuite cet événement pour déterminer quand les hologrammes ne peuvent pas être rendus à l’stationnaire dans le monde.</span><span class="sxs-lookup"><span data-stu-id="b8f03-178">Then use this event to determine when holograms cannot be rendered stationary to the world.</span></span>

## <a name="see-also"></a><span data-ttu-id="b8f03-179">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="b8f03-179">See also</span></span>
* [<span data-ttu-id="b8f03-180">Rendu dans DirectX</span><span class="sxs-lookup"><span data-stu-id="b8f03-180">Rendering in DirectX</span></span>](rendering-in-directx.md)
* [<span data-ttu-id="b8f03-181">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="b8f03-181">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
