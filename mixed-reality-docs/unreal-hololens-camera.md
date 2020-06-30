---
title: Appareil photo/vidéo HoloLens dans Unreal
description: Guide d’utilisation de l’appareil photo/vidéo HoloLens dans Unreal
author: hferrone
ms.author: v-haferr
ms.date: 06/10/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, caméra, appareil photo/vidéo, capture de Réalité Mixte
ms.openlocfilehash: e15ea593283a22dc31cd496de596159035d83799
ms.sourcegitcommit: 45da0a056fa42088ff81ccdd11232830fbe8430f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84720325"
---
# <a name="hololens-photovideo-camera-in-unreal"></a><span data-ttu-id="1994a-104">Appareil photo/vidéo HoloLens dans Unreal</span><span class="sxs-lookup"><span data-stu-id="1994a-104">HoloLens Photo/Video Camera in Unreal</span></span>

## <a name="overview"></a><span data-ttu-id="1994a-105">Vue d’ensemble</span><span class="sxs-lookup"><span data-stu-id="1994a-105">Overview</span></span>

<span data-ttu-id="1994a-106">HoloLens propose un appareil photo/vidéo qui est utilisé pour la capture de Réalité Mixte, et qui peut également être utilisé par une application pour accéder à des visuels du monde réel.</span><span class="sxs-lookup"><span data-stu-id="1994a-106">The HoloLens has a Photo/Video (PV) Camera that is used for both Mixed Reality Capture (MRC) and can be used by an app to access real-world visuals.</span></span>

## <a name="render-from-the-pv-camera-for-mrc"></a><span data-ttu-id="1994a-107">Affichage à partir de l’appareil photo/vidéo pour la capture de Réalité Mixte</span><span class="sxs-lookup"><span data-stu-id="1994a-107">Render from the PV Camera for MRC</span></span>

> [!NOTE]
> <span data-ttu-id="1994a-108">Cela nécessite **Unreal Engine 4.25** ou ultérieur.</span><span class="sxs-lookup"><span data-stu-id="1994a-108">This requires **Unreal Engine 4.25** or newer.</span></span>

<span data-ttu-id="1994a-109">Le système et les enregistreurs personnalisés créent des captures de Réalité Mixte en combinant l’appareil photo/vidéo à des hologrammes affichés par l’application immersive.</span><span class="sxs-lookup"><span data-stu-id="1994a-109">The system, and custom MRC recorders, create mixed reality captures by combining the PV Camera with holograms rendered by the immersive app.</span></span>

<span data-ttu-id="1994a-110">Par défaut, la capture de Réalité Mixte utilise la sortie holographique de l’œil droit.</span><span class="sxs-lookup"><span data-stu-id="1994a-110">By default, mixed reality capture uses the right eye's holographic output.</span></span> <span data-ttu-id="1994a-111">Si une application immersive choisit de s’[afficher à partir de l’appareil photo/vidéo](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in), alors cette sortie sera utilisée à la place.</span><span class="sxs-lookup"><span data-stu-id="1994a-111">If an immersive app chooses to [render from the PV Camera](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in) then that will be used instead.</span></span> <span data-ttu-id="1994a-112">Cela améliore le mappage entre le monde réel et les hologrammes dans la vidéo MRC.</span><span class="sxs-lookup"><span data-stu-id="1994a-112">This improves the mapping between the real world and the holograms in the MRC video.</span></span>

<span data-ttu-id="1994a-113">Pour choisir le rendu à partir de l’appareil photo/vidéo :</span><span class="sxs-lookup"><span data-stu-id="1994a-113">To opt-in to rendering from the PV Camera:</span></span>

1. <span data-ttu-id="1994a-114">Appelez **SetEnabledMixedRealityCamera** et **ResizeMixedRealityCamera**</span><span class="sxs-lookup"><span data-stu-id="1994a-114">Call **SetEnabledMixedRealityCamera** and **ResizeMixedRealityCamera**</span></span>
    * <span data-ttu-id="1994a-115">Utilisez les valeurs de taille **Size X** et **Size Y** pour définir les dimensions de la vidéo.</span><span class="sxs-lookup"><span data-stu-id="1994a-115">Use the **Size X** and **Size Y** values to set the video dimensions.</span></span>

![Troisième caméra](images/unreal-camera-3rd.PNG)

<span data-ttu-id="1994a-117">Unreal va ensuite gérer les requêtes de capture de Réalité Mixte pour effectuer le rendu du point de vue de l’appareil photo/vidéo.</span><span class="sxs-lookup"><span data-stu-id="1994a-117">Unreal will then handle requests from MRC to render from the PV Camera's perspective.</span></span>

> [!NOTE]
> <span data-ttu-id="1994a-118">C’est seulement quand la [capture de Réalité Mixte](mixed-reality-capture.md) est déclenchée qu’il est demandé à l’application de s’afficher du point de vue de l’appareil photo/vidéo.</span><span class="sxs-lookup"><span data-stu-id="1994a-118">Only when [Mixed Reality Capture](mixed-reality-capture.md) is triggered will the app be asked to render from the photo/video camera's perspective.</span></span>

## <a name="using-the-pv-camera"></a><span data-ttu-id="1994a-119">Utilisation de l’appareil photo/vidéo</span><span class="sxs-lookup"><span data-stu-id="1994a-119">Using the PV Camera</span></span>

<span data-ttu-id="1994a-120">La texture de la webcam peut être récupérée dans le jeu au moment de l’exécution. Toutefois, vous devez l’activer dans l’éditeur **Edit > Project Settings** (Modifier > Paramètres du projet) :</span><span class="sxs-lookup"><span data-stu-id="1994a-120">The webcam texture can be retrieved in the game at runtime, but it needs to be enabled in the editor's **Edit > Project Settings**:</span></span>
1. <span data-ttu-id="1994a-121">Accédez à **Platforms > HoloLens > Capabilities** (Plateformes > HoloLens > Fonctionnalités), puis cochez **Webcam**.</span><span class="sxs-lookup"><span data-stu-id="1994a-121">Go to **Platforms > HoloLens > Capabilities** and check **Webcam**.</span></span>
    * <span data-ttu-id="1994a-122">Utilisez la fonction **StartCameraCapture** pour utiliser la webcam au moment de l’exécution, et la fonction **StopCameraCapture** pour arrêter l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="1994a-122">Use the **StartCameraCapture** function to use the webcam at runtime and the **StopCameraCapture** function to stop recording.</span></span>

![Démarrer/Arrêter la caméra](images/unreal-camera-startstop.PNG)

## <a name="rendering-an-image"></a><span data-ttu-id="1994a-124">Affichage d’une image</span><span class="sxs-lookup"><span data-stu-id="1994a-124">Rendering an image</span></span>
<span data-ttu-id="1994a-125">Pour afficher l’image de l’appareil photo :</span><span class="sxs-lookup"><span data-stu-id="1994a-125">To render the camera image:</span></span>
1. <span data-ttu-id="1994a-126">Créez une instance de matériau dynamique basée sur un matériau du projet, nommé **PVCamMat** dans la capture d’écran ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="1994a-126">Create a dynamic material instance based on a material in the project, which is named **PVCamMat** in the screenshot below.</span></span>  
2. <span data-ttu-id="1994a-127">Définissez l’instance de matériau dynamique sur une variable **Material Instance Dynamic Object Reference**.</span><span class="sxs-lookup"><span data-stu-id="1994a-127">Set the dynamic material instance to a **Material Instance Dynamic Object Reference** variable.</span></span>  
3. <span data-ttu-id="1994a-128">Définissez le matériau de l’objet de la scène qui affichera le flux de l’appareil sur cette nouvelle instance de matériau dynamique.</span><span class="sxs-lookup"><span data-stu-id="1994a-128">Set the material of the object in the scene that will render the camera feed to this new dynamic material instance.</span></span>
    * <span data-ttu-id="1994a-129">Démarrez un minuteur qui sera utilisé pour lier l’image de l’appareil au matériau.</span><span class="sxs-lookup"><span data-stu-id="1994a-129">Start a timer that will be used to bind the camera image to the material.</span></span> 

![Rendu de la caméra](images/unreal-camera-render.PNG)

4. <span data-ttu-id="1994a-131">Créez une fonction pour ce minuteur, dans ce cas **MaterialTimer**, puis appelez **GetARCameraImage** pour obtenir la texture à partir de la webcam.</span><span class="sxs-lookup"><span data-stu-id="1994a-131">Create a new function for this timer, in this case **MaterialTimer**, and call **GetARCameraImage** to get the texture from the webcam.</span></span>  
5. <span data-ttu-id="1994a-132">Si la texture est correcte, définissez un paramètre de texture dans le nuanceur de cette image.</span><span class="sxs-lookup"><span data-stu-id="1994a-132">If the texture is valid, set a texture parameter in the shader to the image.</span></span>  <span data-ttu-id="1994a-133">Sinon, redémarrez le minuteur de matériau.</span><span class="sxs-lookup"><span data-stu-id="1994a-133">Otherwise, start the material timer again.</span></span> 

![Texture de la caméra](images/unreal-camera-texture.PNG)

5. <span data-ttu-id="1994a-135">Vérifiez que le matériau comprend un paramètre correspondant au nom situé dans **SetTextureParameterValue**, qui est lié à une entrée de couleur.</span><span class="sxs-lookup"><span data-stu-id="1994a-135">Make sure the material has a parameter matching the name in **SetTextureParameterValue** that's bound to a color entry.</span></span> <span data-ttu-id="1994a-136">Sans cela, l’image de l’appareil photo/vidéo ne pourra pas être affichée correctement.</span><span class="sxs-lookup"><span data-stu-id="1994a-136">Without this, the camera image can't be properly displayed.</span></span>

![Texture de la caméra](images/unreal-camera-material.PNG)

## <a name="see-also"></a><span data-ttu-id="1994a-138">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="1994a-138">See also</span></span>
* [<span data-ttu-id="1994a-139">Appareil photo localisable</span><span class="sxs-lookup"><span data-stu-id="1994a-139">Locatable camera</span></span>](locatable-camera.md)
* [<span data-ttu-id="1994a-140">Capture de Réalité Mixte pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="1994a-140">Mixed reality capture for developers</span></span>](mixed-reality-capture-for-developers.md)
