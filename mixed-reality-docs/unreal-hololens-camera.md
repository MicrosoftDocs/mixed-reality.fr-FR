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
# <a name="hololens-photovideo-camera-in-unreal"></a>Appareil photo/vidéo HoloLens dans Unreal

## <a name="overview"></a>Vue d’ensemble

HoloLens propose un appareil photo/vidéo qui est utilisé pour la capture de Réalité Mixte, et qui peut également être utilisé par une application pour accéder à des visuels du monde réel.

## <a name="render-from-the-pv-camera-for-mrc"></a>Affichage à partir de l’appareil photo/vidéo pour la capture de Réalité Mixte

> [!NOTE]
> Cela nécessite **Unreal Engine 4.25** ou ultérieur.

Le système et les enregistreurs personnalisés créent des captures de Réalité Mixte en combinant l’appareil photo/vidéo à des hologrammes affichés par l’application immersive.

Par défaut, la capture de Réalité Mixte utilise la sortie holographique de l’œil droit. Si une application immersive choisit de s’[afficher à partir de l’appareil photo/vidéo](mixed-reality-capture-for-developers.md#render-from-the-pv-camera-opt-in), alors cette sortie sera utilisée à la place. Cela améliore le mappage entre le monde réel et les hologrammes dans la vidéo MRC.

Pour choisir le rendu à partir de l’appareil photo/vidéo :

1. Appelez **SetEnabledMixedRealityCamera** et **ResizeMixedRealityCamera**
    * Utilisez les valeurs de taille **Size X** et **Size Y** pour définir les dimensions de la vidéo.

![Troisième caméra](images/unreal-camera-3rd.PNG)

Unreal va ensuite gérer les requêtes de capture de Réalité Mixte pour effectuer le rendu du point de vue de l’appareil photo/vidéo.

> [!NOTE]
> C’est seulement quand la [capture de Réalité Mixte](mixed-reality-capture.md) est déclenchée qu’il est demandé à l’application de s’afficher du point de vue de l’appareil photo/vidéo.

## <a name="using-the-pv-camera"></a>Utilisation de l’appareil photo/vidéo

La texture de la webcam peut être récupérée dans le jeu au moment de l’exécution. Toutefois, vous devez l’activer dans l’éditeur **Edit > Project Settings** (Modifier > Paramètres du projet) :
1. Accédez à **Platforms > HoloLens > Capabilities** (Plateformes > HoloLens > Fonctionnalités), puis cochez **Webcam**.
    * Utilisez la fonction **StartCameraCapture** pour utiliser la webcam au moment de l’exécution, et la fonction **StopCameraCapture** pour arrêter l’enregistrement.

![Démarrer/Arrêter la caméra](images/unreal-camera-startstop.PNG)

## <a name="rendering-an-image"></a>Affichage d’une image
Pour afficher l’image de l’appareil photo :
1. Créez une instance de matériau dynamique basée sur un matériau du projet, nommé **PVCamMat** dans la capture d’écran ci-dessous.  
2. Définissez l’instance de matériau dynamique sur une variable **Material Instance Dynamic Object Reference**.  
3. Définissez le matériau de l’objet de la scène qui affichera le flux de l’appareil sur cette nouvelle instance de matériau dynamique.
    * Démarrez un minuteur qui sera utilisé pour lier l’image de l’appareil au matériau. 

![Rendu de la caméra](images/unreal-camera-render.PNG)

4. Créez une fonction pour ce minuteur, dans ce cas **MaterialTimer**, puis appelez **GetARCameraImage** pour obtenir la texture à partir de la webcam.  
5. Si la texture est correcte, définissez un paramètre de texture dans le nuanceur de cette image.  Sinon, redémarrez le minuteur de matériau. 

![Texture de la caméra](images/unreal-camera-texture.PNG)

5. Vérifiez que le matériau comprend un paramètre correspondant au nom situé dans **SetTextureParameterValue**, qui est lié à une entrée de couleur. Sans cela, l’image de l’appareil photo/vidéo ne pourra pas être affichée correctement.

![Texture de la caméra](images/unreal-camera-material.PNG)

## <a name="see-also"></a>Voir aussi
* [Appareil photo localisable](locatable-camera.md)
* [Capture de Réalité Mixte pour les développeurs](mixed-reality-capture-for-developers.md)
