---
title: Caméra HoloLens dans Unreal
description: Guide d’utilisation de la caméra HoloLens dans Unreal
author: sw5813
ms.author: jacksonf
ms.date: 5/5/2020
ms.topic: article
ms.localizationpriority: high
keywords: Unreal, Unreal Engine 4, UE4, HoloLens, HoloLens 2, réalité mixte, développement, fonctionnalités, documentation, guides, hologrammes, caméra, troisième caméra, MRC
ms.openlocfilehash: 9ef9ce27d161130c6b9f3aa6bb1dbc47d7608ad9
ms.sourcegitcommit: ba4c8c2a19bd6a9a181b2cec3cb8e0402f8cac62
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82840118"
---
# <a name="hololens-camera-in-unreal"></a><span data-ttu-id="58cd8-104">Caméra HoloLens dans Unreal</span><span class="sxs-lookup"><span data-stu-id="58cd8-104">HoloLens Camera in Unreal</span></span>

## <a name="third-camera-mixed-reality-capture"></a><span data-ttu-id="58cd8-105">Troisième caméra Mixed Reality Capture (MRC)</span><span class="sxs-lookup"><span data-stu-id="58cd8-105">Third Camera Mixed Reality Capture</span></span>

<span data-ttu-id="58cd8-106">La troisième caméra Mixed Reality Capture (MRC) permet de restituer une capture de réalité mixte du point de vue de la caméra sur le viseur HoloLens, plutôt que de la perspective des textures oculaires.</span><span class="sxs-lookup"><span data-stu-id="58cd8-106">Third camera Mixed Reality Capture (MRC) can be used to render a mixed reality capture from the perspective of the camera on the HoloLens visor, rather than the perspective of the eye textures.</span></span>  <span data-ttu-id="58cd8-107">Cela améliore le mappage entre le monde réel et les hologrammes dans la vidéo MRC.</span><span class="sxs-lookup"><span data-stu-id="58cd8-107">This improves the mapping between the real world and the holograms in the MRC video.</span></span> 

<span data-ttu-id="58cd8-108">Pour activer l’utilisation de la troisième caméra MRC, appelez SetEnabledMixedRealityCamera et ResizeMixedRealityCamera en spécifiant les dimensions vidéo souhaitées.</span><span class="sxs-lookup"><span data-stu-id="58cd8-108">To opt into using third camera MRC, call SetEnabledMixedRealityCamera and ResizeMixedRealityCamera with the desired video dimensions.</span></span> 

![Troisième caméra](images/unreal-camera-3rd.PNG)

<span data-ttu-id="58cd8-110">Enregistrez ensuite une vidéo MRC dans le portail d’appareil pour HoloLens.</span><span class="sxs-lookup"><span data-stu-id="58cd8-110">Then record an MRC video in the HoloLens device portal.</span></span> 

## <a name="pv-camera"></a><span data-ttu-id="58cd8-111">Caméra PV</span><span class="sxs-lookup"><span data-stu-id="58cd8-111">PV Camera</span></span>

<span data-ttu-id="58cd8-112">La texture de la webcam peut également être récupérée dans le jeu au moment de l’exécution.</span><span class="sxs-lookup"><span data-stu-id="58cd8-112">The webcam texture can also be retrieved in the game at runtime.</span></span>  <span data-ttu-id="58cd8-113">Pour obtenir la texture de la webcam sur HoloLens, vérifiez d’abord que la fonctionnalité « Webcam » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities.</span><span class="sxs-lookup"><span data-stu-id="58cd8-113">To get the webcam texture on HoloLens, first ensure the “Webcam” capability is checked in the Unreal editor under Project Settings > Platform > HoloLens > Capabilities.</span></span> 

<span data-ttu-id="58cd8-114">Activez l’utilisation de la webcam au moment de l’exécution avec la fonction StartCameraCapture.</span><span class="sxs-lookup"><span data-stu-id="58cd8-114">Opt into using the webcam at runtime with the StartCameraCapture function.</span></span>  <span data-ttu-id="58cd8-115">Arrêtez la capture avec la fonction StopCameraCapture.</span><span class="sxs-lookup"><span data-stu-id="58cd8-115">Stop capturing with the StopCameraCapture function.</span></span> 

![Démarrer/Arrêter la caméra](images/unreal-camera-startstop.PNG)

<span data-ttu-id="58cd8-117">Pour le rendu de l’image de la caméra, créez d’abord une instance de matériau dynamique basée sur un matériau dans le projet.</span><span class="sxs-lookup"><span data-stu-id="58cd8-117">To render the camera image, first create a dynamic material instance based on a material in the project.</span></span>  <span data-ttu-id="58cd8-118">Dans cet exemple, l’instance est basée sur un matériau nommé PVCamMat.</span><span class="sxs-lookup"><span data-stu-id="58cd8-118">In this case based on a material named PVCamMat.</span></span>  <span data-ttu-id="58cd8-119">Affectez-lui une variable de type « Material Instance Dynamic Object Reference ».</span><span class="sxs-lookup"><span data-stu-id="58cd8-119">Set this to a variable with type Material Instance Dynamic Object Reference.</span></span>  <span data-ttu-id="58cd8-120">Définissez ensuite le matériau de l’objet dans la scène du rendu du flux de la caméra sur cette nouvelle instance de matériel dynamique, et démarrez un minuteur qui sera utilisé pour lier l’image de la caméra au matériau.</span><span class="sxs-lookup"><span data-stu-id="58cd8-120">Then set the material of the object in the scene that will render the camera feed to this new dynamic material instance and start a timer that will be used to bind the camera image to the material.</span></span> 

![Rendu de la caméra](images/unreal-camera-render.PNG)

<span data-ttu-id="58cd8-122">Créez une fonction pour ce minuteur, MaterialTimer ici, puis appelez GetARCameraImage pour obtenir la texture à partir de la webcam.</span><span class="sxs-lookup"><span data-stu-id="58cd8-122">Create a new function for this timer, in this case MaterialTimer, and call GetARCameraImage to get the texture from the webcam.</span></span>  <span data-ttu-id="58cd8-123">Si cette texture est correcte, définissez un paramètre de texture dans le nuanceur sur cette image.</span><span class="sxs-lookup"><span data-stu-id="58cd8-123">If this texture is valid, set a texture parameter in the shader to this image.</span></span>  <span data-ttu-id="58cd8-124">Sinon, redémarrez le minuteur de matériau.</span><span class="sxs-lookup"><span data-stu-id="58cd8-124">Otherwise, start the material timer again.</span></span> 

![Texture de la caméra](images/unreal-camera-texture.PNG)

<span data-ttu-id="58cd8-126">Le matériau doit avoir un paramètre correspondant au nom dans SetTextureParameterValue associé à une entrée de couleur pour afficher correctement l’image de la caméra.</span><span class="sxs-lookup"><span data-stu-id="58cd8-126">The material should have a parameter matching the name in SetTextureParameterValue bound to a color entry to properly display the camera image.</span></span> 

![Texture de la caméra](images/unreal-camera-material.PNG)

## <a name="see-also"></a><span data-ttu-id="58cd8-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="58cd8-128">See also</span></span>
* [<span data-ttu-id="58cd8-129">Appareil photo localisable</span><span class="sxs-lookup"><span data-stu-id="58cd8-129">Locatable camera</span></span>](locatable-camera.md)
* [<span data-ttu-id="58cd8-130">Capture de Réalité Mixte pour les développeurs</span><span class="sxs-lookup"><span data-stu-id="58cd8-130">Mixed reality capture for developers</span></span>](mixed-reality-capture-for-developers.md)
