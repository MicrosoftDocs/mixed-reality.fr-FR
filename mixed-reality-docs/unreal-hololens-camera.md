---
title: Appareil photo/vidéo HoloLens dans Unreal
description: Guide d’utilisation de l’appareil photo/vidéo HoloLens dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, caméra, appareil photo/vidéo, capture de Réalité Mixte
ms.openlocfilehash: 06ceb26d58fe60848e5e90360aa2e05984a901c5
ms.sourcegitcommit: f24ac845e184c2f90e8b15adab9addb913f5cb83
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84451334"
---
# <a name="hololens-photovideo-camera-in-unreal"></a><span data-ttu-id="1c757-104">Appareil photo/vidéo HoloLens dans Unreal</span><span class="sxs-lookup"><span data-stu-id="1c757-104">HoloLens Photo/Video Camera in Unreal</span></span>

<span data-ttu-id="1c757-105">HoloLens propose un appareil photo/vidéo qui est utilisé pour la capture de Réalité Mixte, et qui peut également être utilisé par une application pour accéder à des visuels du monde réel.</span><span class="sxs-lookup"><span data-stu-id="1c757-105">The HoloLens has a Photo/Video (PV) Camera that is used for both Mixed Reality Capture (MRC) and can be used by an app to access real-world visuals.</span></span>

## <a name="render-from-the-pv-camera-for-mrc"></a><span data-ttu-id="1c757-106">Affichage à partir de l’appareil photo/vidéo pour la capture de Réalité Mixte</span><span class="sxs-lookup"><span data-stu-id="1c757-106">Render from the PV Camera for MRC</span></span>

> [!NOTE]
> <span data-ttu-id="1c757-107">Cela nécessite **Unreal Engine 4.25** ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1c757-107">This requires **Unreal Engine 4.25** or newer.</span></span>

<span data-ttu-id="1c757-108">Le système et les enregistreurs personnalisés créent des captures de Réalité Mixte en combinant l’appareil photo/vidéo à des hologrammes affichés par l’application immersive.</span><span class="sxs-lookup"><span data-stu-id="1c757-108">The system, and custom MRC recorders, create mixed reality captures by combining the PV Camera with holograms rendered by the immersive app.</span></span>

<span data-ttu-id="1c757-109">Par défaut, la capture de Réalité Mixte utilise la sortie holographique de l’œil droit.</span><span class="sxs-lookup"><span data-stu-id="1c757-109">By default, mixed reality capture uses the right eye's holographic output.</span></span> <span data-ttu-id="1c757-110">Si une application immersive choisit de s’[afficher à partir de l’appareil photo/vidéo](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in), alors cette sortie sera utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="1c757-110">If an immersive app chooses to [render from the PV Camera](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) then that will be used instead.</span></span> <span data-ttu-id="1c757-111">Cela améliore le mappage entre le monde réel et les hologrammes dans la vidéo MRC.</span><span class="sxs-lookup"><span data-stu-id="1c757-111">This improves the mapping between the real world and the holograms in the MRC video.</span></span>

<span data-ttu-id="1c757-112">Pour choisir le rendu à partir de l’appareil photo/vidéo :</span><span class="sxs-lookup"><span data-stu-id="1c757-112">To opt-in to rendering from the PV Camera:</span></span>

1. <span data-ttu-id="1c757-113">Appelez **SetEnabledMixedRealityCamera** et **ResizeMixedRealityCamera**</span><span class="sxs-lookup"><span data-stu-id="1c757-113">Call **SetEnabledMixedRealityCamera** and **ResizeMixedRealityCamera**</span></span>
    * <span data-ttu-id="1c757-114">Utilisez les valeurs de taille **Size X** et **Size Y** pour définir les dimensions de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="1c757-114">Use the **Size X** and **Size Y** values to set the video dimensions.</span></span>

![Troisième caméra](images/unreal-camera-3rd.PNG)

<span data-ttu-id="1c757-116">Unreal va ensuite gérer les requêtes de capture de Réalité Mixte pour effectuer le rendu du point de vue de l’appareil photo/vidéo.</span><span class="sxs-lookup"><span data-stu-id="1c757-116">Unreal will then handle requests from MRC to render from the PV Camera's perspective.</span></span>

> [!NOTE]
> <span data-ttu-id="1c757-117">C’est seulement quand la [capture de Réalité Mixte](mixed-reality-capture.md) est déclenchée qu’il est demandé à l’application de s’afficher du point de vue de l’appareil photo/vidéo.</span><span class="sxs-lookup"><span data-stu-id="1c757-117">Only when [Mixed Reality Capture](mixed-reality-capture.md) is triggered will the app be asked to render from the photo/video camera's perspective.</span></span>

## <a name="using-the-pv-camera"></a><span data-ttu-id="1c757-118">Utilisation de l’appareil photo/vidéo</span><span class="sxs-lookup"><span data-stu-id="1c757-118">Using the PV Camera</span></span>

<span data-ttu-id="1c757-119">La texture de la webcam peut être récupérée dans le jeu au moment de l’exécution. Toutefois, vous devez l’activer dans l’éditeur **Edit > Project Settings** (Modifier > Paramètres du projet) :</span><span class="sxs-lookup"><span data-stu-id="1c757-119">The webcam texture can be retrieved in the game at runtime, but it needs to be enabled in the editor's **Edit > Project Settings**:</span></span>
1. <span data-ttu-id="1c757-120">Accédez à **Platforms > HoloLens > Capabilities** (Plateformes > HoloLens > Fonctionnalités), puis cochez **Webcam**.</span><span class="sxs-lookup"><span data-stu-id="1c757-120">Go to **Platforms > HoloLens > Capabilities** and check **Webcam**.</span></span>
    * <span data-ttu-id="1c757-121">Utilisez la fonction **StartCameraCapture** pour utiliser la webcam au moment de l’exécution, et la fonction **StopCameraCapture** pour arrêter l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="1c757-121">Use the **StartCameraCapture** function to use the webcam at runtime and the **StopCameraCapture** function to stop recording.</span></span>

![Démarrer/Arrêter la caméra](images/unreal-camera-startstop.PNG)

## <a name="rendering-an-image"></a><span data-ttu-id="1c757-123">Affichage d’une image</span><span class="sxs-lookup"><span data-stu-id="1c757-123">Rendering an image</span></span>
<span data-ttu-id="1c757-124">Pour afficher l’image de l’appareil photo :</span><span class="sxs-lookup"><span data-stu-id="1c757-124">To render the camera image:</span></span>
1. <span data-ttu-id="1c757-125">Créez une instance de matériau dynamique basée sur un matériau du projet, nommé **PVCamMat** dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1c757-125">Create a dynamic material instance based on a material in the project, which is named **PVCamMat** in the screenshot below.</span></span>  
2. <span data-ttu-id="1c757-126">Définissez l’instance de matériau dynamique sur une variable **Material Instance Dynamic Object Reference**.</span><span class="sxs-lookup"><span data-stu-id="1c757-126">Set the dynamic material instance to a **Material Instance Dynamic Object Reference** variable.</span></span>  
3. <span data-ttu-id="1c757-127">Définissez le matériau de l’objet de la scène qui affichera le flux de l’appareil sur cette nouvelle instance de matériau dynamique.</span><span class="sxs-lookup"><span data-stu-id="1c757-127">Set the material of the object in the scene that will render the camera feed to this new dynamic material instance.</span></span>
    * <span data-ttu-id="1c757-128">Démarrez un minuteur qui sera utilisé pour lier l’image de l’appareil au matériau.</span><span class="sxs-lookup"><span data-stu-id="1c757-128">Start a timer that will be used to bind the camera image to the material.</span></span> 

![Rendu de la caméra](images/unreal-camera-render.PNG)

4. <span data-ttu-id="1c757-130">Créez une fonction pour ce minuteur, dans ce cas **MaterialTimer**, puis appelez **GetARCameraImage** pour obtenir la texture à partir de la webcam.</span><span class="sxs-lookup"><span data-stu-id="1c757-130">Create a new function for this timer, in this case **MaterialTimer**, and call **GetARCameraImage** to get the texture from the webcam.</span></span>  
5. <span data-ttu-id="1c757-131">Si la texture est correcte, définissez un paramètre de texture dans le nuanceur de cette image.</span><span class="sxs-lookup"><span data-stu-id="1c757-131">If the texture is valid, set a texture parameter in the shader to the image.</span></span>  <span data-ttu-id="1c757-132">Sinon, redémarrez le minuteur de matériau.</span><span class="sxs-lookup"><span data-stu-id="1c757-132">Otherwise, start the material timer again.</span></span> 

![Texture de la caméra](images/unreal-camera-texture.PNG)

5. <span data-ttu-id="1c757-134">Vérifiez que le matériau comprend un paramètre correspondant au nom situé dans **SetTextureParameterValue**, qui est lié à une entrée de couleur.</span><span class="sxs-lookup"><span data-stu-id="1c757-134">Make sure the material has a parameter matching the name in **SetTextureParameterValue** that's bound to a color entry.</span></span> <span data-ttu-id="1c757-135">Sans cela, l’image de l’appareil photo/vidéo ne pourra pas être affichée correctement.</span><span class="sxs-lookup"><span data-stu-id="1c757-135">Without this, the camera image can't be properly displayed.</span></span>

![Texture de la caméra](images/unreal-camera-material.PNG)

## <a name="see-also"></a><span data-ttu-id="1c757-137">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1c757-137">See also</span></span>
* [<span data-ttu-id="1c757-138">Appareil photo localisable</span><span class="sxs-lookup"><span data-stu-id="1c757-138">Locatable camera</span></span>](locatable-camera.md)
* [<span data-ttu-id="1c757-139">Capture de Réalité Mixte pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="1c757-139">Mixed reality capture for developers</span></span>](mixed-reality-capture-for-developers.md)
