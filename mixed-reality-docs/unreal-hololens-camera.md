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
# <a name="hololens-camera-in-unreal"></a>Caméra HoloLens dans Unreal

## <a name="third-camera-mixed-reality-capture"></a>Troisième caméra Mixed Reality Capture (MRC)

La troisième caméra Mixed Reality Capture (MRC) permet de restituer une capture de réalité mixte du point de vue de la caméra sur le viseur HoloLens, plutôt que de la perspective des textures oculaires.  Cela améliore le mappage entre le monde réel et les hologrammes dans la vidéo MRC. 

Pour activer l’utilisation de la troisième caméra MRC, appelez SetEnabledMixedRealityCamera et ResizeMixedRealityCamera en spécifiant les dimensions vidéo souhaitées. 

![Troisième caméra](images/unreal-camera-3rd.PNG)

Enregistrez ensuite une vidéo MRC dans le portail d’appareil pour HoloLens. 

## <a name="pv-camera"></a>Caméra PV

La texture de la webcam peut également être récupérée dans le jeu au moment de l’exécution.  Pour obtenir la texture de la webcam sur HoloLens, vérifiez d’abord que la fonctionnalité « Webcam » est cochée dans l’éditeur Unreal sous Project Settings > Platform > HoloLens > Capabilities. 

Activez l’utilisation de la webcam au moment de l’exécution avec la fonction StartCameraCapture.  Arrêtez la capture avec la fonction StopCameraCapture. 

![Démarrer/Arrêter la caméra](images/unreal-camera-startstop.PNG)

Pour le rendu de l’image de la caméra, créez d’abord une instance de matériau dynamique basée sur un matériau dans le projet.  Dans cet exemple, l’instance est basée sur un matériau nommé PVCamMat.  Affectez-lui une variable de type « Material Instance Dynamic Object Reference ».  Définissez ensuite le matériau de l’objet dans la scène du rendu du flux de la caméra sur cette nouvelle instance de matériel dynamique, et démarrez un minuteur qui sera utilisé pour lier l’image de la caméra au matériau. 

![Rendu de la caméra](images/unreal-camera-render.PNG)

Créez une fonction pour ce minuteur, MaterialTimer ici, puis appelez GetARCameraImage pour obtenir la texture à partir de la webcam.  Si cette texture est correcte, définissez un paramètre de texture dans le nuanceur sur cette image.  Sinon, redémarrez le minuteur de matériau. 

![Texture de la caméra](images/unreal-camera-texture.PNG)

Le matériau doit avoir un paramètre correspondant au nom dans SetTextureParameterValue associé à une entrée de couleur pour afficher correctement l’image de la caméra. 

![Texture de la caméra](images/unreal-camera-material.PNG)

## <a name="see-also"></a>Voir aussi
* [Appareil photo localisable](locatable-camera.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
