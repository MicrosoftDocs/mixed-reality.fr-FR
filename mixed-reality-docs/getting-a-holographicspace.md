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
# <a name="getting-a-holographicspace"></a>Obtention d’un HolographicSpace

Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> classe est votre portail dans le monde HOLOGRAPHIQUE. Il contrôle rendu immersif, fournit des données de l’appareil photo et fournit l’accès aux API de raisonnement spatiale. Vous allez créer une pour votre application UWP <a href="https://docs.microsoft.com/api/windows.ui.core.corewindow" target="_blank">CoreWindow</a> ou HWND de votre application Win32.

## <a name="set-up-the-holographic-space"></a>Configurer l’espace HOLOGRAPHIQUE

Création de l’objet espace holographique est la première étape dans votre application Windows Mixed Reality. Les applications Windows traditionnelles restituent à une chaîne de permutation de Direct3D créée pour la fenêtre de base de leur vue de l’application. Cette chaîne de permutation est affichée pour une ardoise dans l’interface utilisateur HOLOGRAPHIQUE. Pour rendre votre vue de l’application HOLOGRAPHIQUE au lieu d’une ardoise 2D, créer un espace HOLOGRAPHIQUE sa fenêtre core au lieu d’une chaîne de permutation. Présentation HOLOGRAPHIQUE frames qui sont créés par cet espace HOLOGRAPHIQUE met votre application en mode de rendu de plein écran.

Pour un **application UWP** [à partir de la *modèle d’application de 11 HOLOGRAPHIQUE DirectX (Windows universel)*](creating-a-holographic-directx-project.md), recherchez ce code dans le **SetWindow** méthode dans AppView.cpp :

```cpp
m_holographicSpace = HolographicSpace::CreateForCoreWindow(window);
```

Pour un **application Win32** [à partir de la *BasicHologram* Win32, exemple](creating-a-holographic-directx-project.md#creating-a-win32-project), examinez **App::CreateWindowAndHolographicSpace** pour un exemple montrant comment créer un HWND et le convertir en un HWND immersif en créant associé à un <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a>:
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

Maintenant que vous avez obtenu un HolographicSpace pour votre UWP CoreWindow ou le HWND Win32, vous utiliserez ce HolographicSpace pour gérer les caméras HOLOGRAPHIQUE, créer des systèmes de coordonnées et effectuer le rendu HOLOGRAPHIQUE. L’espace HOLOGRAPHIQUE actuel est utilisé dans plusieurs endroits dans le modèle de DirectX :
* Le **DeviceResources** classe a besoin d’obtenir des informations à partir de l’objet HolographicSpace afin de créer le périphérique Direct3D. Il s’agit de l’ID de carte DXGI associé à l’écran holographique. Le <a href="https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicspace" target="_blank">HolographicSpace</a> classe utilise un appareil de Direct3D 11 de votre application pour créer et gérer des ressources basées sur les appareils, tels que les mémoires tampons d’arrière-plan pour chaque caméra HOLOGRAPHIQUE. Si vous voulez voir ce que fait cette fonction sous le capot, vous la trouverez dans DeviceResources.cpp.
* La fonction **DeviceResources::InitializeUsingHolographicSpace** montre comment obtenir l’adaptateur en recherchant le LUID – et comment choisir un adaptateur par défaut lorsque aucune carte préférée n’est spécifié.
* Classe principale de l’application utilise l’espace holographique de **AppView::SetWindow** ou **App::CreateWindowAndHolographicSpace** pour les mises à jour et de rendu.

>[!NOTE]
>Tandis que les sections ci-dessous mentionner les noms de fonction à partir du modèle comme **AppView::SetWindow** qui supposent que vous avez démarré à partir du modèle d’application UWP HOLOGRAPHIQUE, les extraits de code que vous voyez seront applique également dans les applications UWP et Win32.

Ensuite, nous nous plongerons dans le programme d’installation qui traiter **SetHolographicSpace** est chargé dans la classe AppMain.

## <a name="subscribe-to-camera-events-create-and-remove-camera-resources"></a>S’abonner aux événements de l’appareil photo, créer et supprimer des ressources de l’appareil photo

Contenu holographique de votre application se trouve dans son espace holographique et est affichée via un ou plusieurs caméras HOLOGRAPHIQUE qui représentent différentes perspectives sur la scène. Maintenant que vous avez l’espace HOLOGRAPHIQUE, vous pouvez recevoir des données d’appareils photo HOLOGRAPHIQUE.

Votre application doit répondre aux **CameraAdded** événements en créant toutes les ressources qui sont spécifiques à cet appareil photo, tels que votre mémoire tampon d’arrière-plan restituer la vue cible. Vous pouvez voir ce code dans le **DeviceResources::SetHolographicSpace** fonction, appelée par **AppView::SetWindow** avant que l’application crée des frames HOLOGRAPHIQUE :

```cpp
m_cameraAddedToken = m_holographicSpace.CameraAdded(
    std::bind(&AppMain::OnCameraAdded, this, _1, _2));
```

Votre application doit également répondre aux **CameraRemoved** événements en libérant les ressources qui ont été créés pour cet appareil photo.

À partir de **DeviceResources::SetHolographicSpace**:

```cpp
m_cameraRemovedToken = m_holographicSpace.CameraRemoved(
    std::bind(&AppMain::OnCameraRemoved, this, _1, _2));
```

Les gestionnaires d’événements doivent effectuer certaines tâches afin de conserver l’échange de données, de rendu holographique et afin que votre application est en mesure d’effectuer le rendu du tout. Lire le code et les commentaires pour plus d’informations : vous pouvez rechercher des **OnCameraAdded** et **OnCameraRemoved** dans votre classe principale pour comprendre comment la **m_cameraResources** map est géré par **DeviceResources**.

À ce stade, nous nous concentrons sur AppMain et le programme d’installation qu’il fait pour activer votre application pour connaître les caméras HOLOGRAPHIQUE. Dans cet esprit, il est important de tenir compte des deux conditions suivantes :

1. Pour le **CameraAdded** Gestionnaire d’événements, l’application peut fonctionner de façon asynchrone pour terminer la création de ressources et de chargement d’actifs pour le nouvel appareil photo HOLOGRAPHIQUE. Les applications qui prennent plusieurs frames pour effectuer ce travail doivent demander un report et terminer le report après le chargement asynchrone ; un [tâche PPL](https://docs.microsoft.com/cpp/parallel/concrt/parallel-patterns-library-ppl) peut être utilisé pour faire le travail asynchrone. Votre application doit s’assurer qu’il est prêt pour le rendu à cet appareil photo immédiatement lorsqu’il termine le Gestionnaire d’événements, ou lorsqu’il s’achève le report. Fermeture du Gestionnaire d’événements ou à la fin du report indique au système que votre application est maintenant prête à recevoir des trames holographique avec cette photo inclus.

2. Lorsque l’application reçoit un **CameraRemoved** événement, il doit libérer toutes les références à la mémoire tampon d’arrière-plan et la quitter immédiatement et la fonction. Cela inclut les vues de cible de rendu et toute autre ressource que peut contenir une référence à la [IDXGIResource](https://docs.microsoft.com/windows/desktop/api/dxgi/nn-dxgi-idxgiresource). L’application doit également s’assurer que la mémoire tampon d’arrière-plan n’est pas attaché en tant que cible de rendu, comme indiqué dans **CameraResources::ReleaseResourcesForBackBuffer**. Pour aider à accélérer le processus long, votre application peut libérer la mémoire tampon d’arrière-plan, puis lancer une tâche pour terminer de façon asynchrone n’importe quel autre travail n’est nécessaire de détruire ce appareil photo. Le modèle d’application HOLOGRAPHIQUE inclut une tâche PPL que vous pouvez utiliser à cet effet.

>[!NOTE]
>Si vous souhaitez déterminer quand une caméra ajoutée ou supprimée apparaît sur l’image, utilisez le **HolographicFrame** [AddedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.addedcameras) et [RemovedCameras](https://docs.microsoft.com/uwp/api/windows.graphics.holographic.holographicframe.removedcameras) propriétés.

## <a name="create-a-frame-of-reference-for-your-holographic-content"></a>Créer un cadre de référence pour votre contenu HOLOGRAPHIQUE

Contenu de votre application doit être positionné dans un [système de coordonnées spatial](coordinate-systems-in-directx.md) à restituer dans le HolographicSpace. Le système fournit deux principal de référence que vous pouvez utiliser pour établir un système de coordonnées pour votre hologrammes.

Il existe deux sortes de trames de référence dans Windows HOLOGRAPHIQUE : référencer les images associées à l’appareil et les trames de référence restent STATIONNAIRES lorsque se trouve l’appareil via l’environnement utilisateur. Le modèle d’application HOLOGRAPHIQUE utilise un cadre de référence stationnaire par défaut ; Il s’agit d’une des manières plus simples pour restituer hologrammes verrouillé de monde.

Trames de référence stationnaire sont conçus pour stabiliser les positions proche de l’emplacement actuel de l’appareil. Cela signifie que les coordonnées plus éloigné de l’appareil sont autorisées à dérives légèrement en ce qui concerne l’environnement utilisateur, comme l’appareil en apprend plus sur l’espace autour de lui. Il existe deux façons de créer un système de référence stationnaire : acquérir le système de coordonnées à partir de la [étape spatial](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), ou utiliser la valeur par défaut <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>. Si vous créez une application Windows Mixed Reality pour des casques IMMERSIFS, le point de départ recommandé est la [étape spatial](coordinate-systems-in-directx.md#place-holograms-in-the-world-using-a-spatial-stage), qui fournit également des informations sur les fonctionnalités du casque immersive porté par le lecteur. Ici, nous montrons comment utiliser la valeur par défaut <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatiallocator" target="_blank">SpatialLocator</a>.

Le localisateur spatial représente le périphérique Windows Mixed Reality et effectue le suivi du mouvement de l’appareil et fournit des systèmes de coordonnées qui peuvent être reconnus par rapport à son emplacement.

À partir de **AppMain::OnHolographicDisplayIsAvailableChanged**:

```cpp
spatialLocator = SpatialLocator::GetDefault();
```

Créer une fois l’image de référence stationnaire lorsque l’application est lancée. Ceci est analogue à la définition d’un système de coordonnées de monde, avec l’origine placé à la position de l’appareil lorsque l’application est lancée. Cette image de référence ne déplace pas avec l’appareil.

À partir de **AppMain::SetHolographicSpace**:

```cpp
m_stationaryReferenceFrame =
    m_spatialLocator.CreateStationaryFrameOfReferenceAtCurrentLocation();
```

Toutes les trames de référence sont gravité aligné, cela signifie que l’axe des y pointe « up » en ce qui concerne l’environnement utilisateur. Étant donné que Windows utilise les systèmes de coordonnées « droitiers », la direction de l’axe z – coïncide avec la direction « forward », que l’appareil est face lors de la création de l’image de référence.

>[!NOTE]
>Lorsque votre application requiert le positionnement précis des hologrammes individuels, utilisez un <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor" target="_blank">SpatialAnchor</a> pour ancrer l’hologramme individuel vers une position dans le monde réel. Par exemple, utiliser un point d’ancrage spatial lorsque l’utilisateur indique un point de présenter un intérêt particulier. Les positions d’ancrage ne pas dérive, mais ils peuvent être ajustés. Par défaut, lorsqu’un point d’ancrage est ajustée, ce qui facilite sa position en place sur les images de plusieurs suivants après la correction. En fonction de votre application, dans ce cas vous souhaiterez traiter l’ajustement d’une manière différente (par exemple en différer jusqu'à ce que l’hologramme n’est pas visible). Le <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystem" target="_blank">RawCoordinateSystem</a> propriété et <a href="https://docs.microsoft.com/uwp/api/windows.perception.spatial.spatialanchor.rawcoordinatesystemadjusted" target="_blank">RawCoordinateSystemAdjusted</a> événements activer ces personnalisations.

## <a name="respond-to-locatability-changed-events"></a>Répondre aux événements de locatability modifié

Rendu hologrammes verrouillé de monde nécessite l’appareil soit en mesure de localiser lui-même dans le monde. Cela n'est pas toujours possible en raison de conditions environnementales, et si tel est le cas, l’utilisateur peut attendre une indication visuelle de l’interruption de suivi. Cette indication visuelle doit être restituée à l’aide d’images de référence associées à l’appareil, au lieu d’arrêt au monde.

Votre application peut demander à être averti si le suivi est interrompu pour une raison quelconque. S’inscrire pour l’événement LocatabilityChanged détecter lorsque la capacité du périphérique à s’y localiser les modifications du monde. À partir de **AppMain::SetHolographicSpace :**

```cpp
m_locatabilityChangedToken = m_spatialLocator.LocatabilityChanged(
    std::bind(&HolographicApp6Main::OnLocatabilityChanged, this, _1, _2));
```

Ensuite, utilisez cet événement pour déterminer quand hologrammes ne peut pas être restitués STATIONNAIRES au monde.

## <a name="see-also"></a>Voir aussi
* [Rendu dans DirectX](rendering-in-directx.md)
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md)
