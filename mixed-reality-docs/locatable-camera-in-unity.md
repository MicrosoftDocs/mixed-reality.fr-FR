---
title: Caméra localisable dans Unity
description: Utilisation de caméra localisables HoloLens dans Unity.
author: wguyman
ms.author: wguyman
ms.date: 03/21/2018
ms.topic: article
keywords: photos, vidéos, hololens, appareil photo, unity, localisable
ms.openlocfilehash: f0183400f55b1c6663a9a20ab4992befe5ad0718
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595116"
---
# <a name="locatable-camera-in-unity"></a>Caméra localisable dans Unity

## <a name="enabling-the-capability-for-photo-video-camera"></a>L’activation de la fonctionnalité pour la caméra vidéo Photo

La fonctionnalité « WebCam » doit être déclarée pour une application d’utiliser le [caméra](locatable-camera.md).
1. Dans l’éditeur Unity, accédez aux paramètres de lecteur en accédant à la page « Modifier > projet Paramètres > lecteur »
2. Cliquez sur l’onglet « Windows Store »
3. Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **WebCam** et **Microphone** fonctionnalités

Seule une opération peut se produire avec l’appareil photo à la fois. Pour déterminer quel mode (photos, vidéo ou aucun) la caméra en cours, vous pouvez vérifier UnityEngine.XR.WSA.WebCam.Mode.

## <a name="photo-capture"></a>Capture de photos

**Namespace :** *UnityEngine.XR.WSA.WebCam*<br>
**Type :** *PhotoCapture*

Le *PhotoCapture* type vous permet de prendre encore photographies avec la caméra vidéo Photo. Le modèle général pour l’utilisation de *PhotoCapture* à prendre une photo est comme suit :
1. Créer un *PhotoCapture* objet
2. Créer un *CameraParameters* objet avec les paramètres que nous voulons
3. Démarrer le Mode de Photo via *StartPhotoModeAsync*
4. Prendre la photo
    * (facultatif) Interagir avec cette image
5. Arrêter le Mode de Photo et de nettoyer les ressources

### <a name="common-set-up-for-photocapture"></a>Ensemble commun de pour PhotoCapture

Pour toutes les utilisations de trois, nous commençons avec le même 3 premières étapes ci-dessus

Nous commençons par créer un *PhotoCapture* objet

```cs
PhotoCapture photoCaptureObject = null;
   void Start()
   {
       PhotoCapture.CreateAsync(false, OnPhotoCaptureCreated);
   }
```

Ensuite nous stocker notre objet défini nos paramètres et démarrer le Mode de la Photo

```cs
void OnPhotoCaptureCreated(PhotoCapture captureObject)
   {
       photoCaptureObject = captureObject;

       Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();

       CameraParameters c = new CameraParameters();
       c.hologramOpacity = 0.0f;
       c.cameraResolutionWidth = cameraResolution.width;
       c.cameraResolutionHeight = cameraResolution.height;
       c.pixelFormat = CapturePixelFormat.BGRA32;

       captureObject.StartPhotoModeAsync(c, false, OnPhotoModeStarted);
   }
```

Au final, nous utiliserons également le même code présenté ici de nettoyage

```cs
void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
   {
       photoCaptureObject.Dispose();
       photoCaptureObject = null;
   }
```

Une fois ces étapes effectuées, vous pouvez choisir le type de la photo pour capturer.

### <a name="capture-a-photo-to-a-file"></a>Capturer une Photo dans un fichier

L’opération la plus simple consiste à capturer une photo directement dans un fichier. La photo peut être enregistrée comme un fichier JPG ou PNG.

Si nous avons commencé avec succès mode photo, nous maintenant prendre une photo et stockez-le sur le disque

```cs
private void OnPhotoModeStarted(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           string filename = string.Format(@"CapturedImage{0}_n.jpg", Time.time);
           string filePath = System.IO.Path.Combine(Application.persistentDataPath, filename);

           photoCaptureObject.TakePhotoAsync(filePath, PhotoCaptureFileOutputFormat.JPG, OnCapturedPhotoToDisk);
       }
       else
       {
           Debug.LogError("Unable to start photo mode!");
       }
   }
```

Après avoir capturé la photo sur le disque, nous quitter le mode de photo et puis nettoyer nos objets

```cs
void OnCapturedPhotoToDisk(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           Debug.Log("Saved Photo to disk!");
           photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
       }
       else
       {
           Debug.Log("Failed to save Photo to disk");
       }
   }
```

### <a name="capture-a-photo-to-a-texture2d"></a>Capturer une Photo à une Texture2D

Lors de la capture des données à une Texture2D, le processus est très similaire à la capture sur le disque.

Nous allons suivre l’ensemble des processus ci-dessus.

Dans *OnPhotoModeStarted*, nous sera capturer un frame dans la mémoire.

```cs
private void OnPhotoModeStarted(PhotoCapture.PhotoCaptureResult result)
   {
       if (result.success)
       {
           photoCaptureObject.TakePhotoAsync(OnCapturedPhotoToMemory);
       }
       else
       {
           Debug.LogError("Unable to start photo mode!");
       }
   }
```

Puis nous appliquer nos résultats à une texture et utiliserons courantes nettoyer le code ci-dessus.

```cs
void OnCapturedPhotoToMemory(PhotoCapture.PhotoCaptureResult result, PhotoCaptureFrame photoCaptureFrame)
   {
       if (result.success)
       {
           // Create our Texture2D for use and set the correct resolution
           Resolution cameraResolution = PhotoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();
           Texture2D targetTexture = new Texture2D(cameraResolution.width, cameraResolution.height);
           // Copy the raw image data into our target texture
           photoCaptureFrame.UploadImageDataToTexture(targetTexture);
           // Do as we wish with the texture such as apply it to a material, etc.
       }
       // Clean up
       photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
   }
```

### <a name="capture-a-photo-and-interact-with-the-raw-bytes"></a>Capturer une Photo et l’interaction avec les octets bruts

Pour interagir avec les octets bruts d’une mémoire frame, nous allons suivre les mêmes étapes que ci-dessus et *OnPhotoModeStarted* comme dans la capture d’une photo à une Texture2D. La différence réside dans *OnCapturedPhotoToMemory* où nous pouvons obtenir les octets bruts et interagir avec eux.

Dans cet exemple, nous allons créer un *liste<Color>*  qui pourrait être plu traité ou appliqués à une texture via *SetPixels()*

```cs
void OnCapturedPhotoToMemory(PhotoCapture.PhotoCaptureResult result, PhotoCaptureFrame photoCaptureFrame)
   {
       if (result.success)
       {
           List<byte> imageBufferList = new List<byte>();
           // Copy the raw IMFMediaBuffer data into our empty byte list.
           photoCaptureFrame.CopyRawImageDataIntoBuffer(imageBufferList);

           // In this example, we captured the image using the BGRA32 format.
           // So our stride will be 4 since we have a byte for each rgba channel.
           // The raw image data will also be flipped so we access our pixel data
           // in the reverse order.
           int stride = 4;
           float denominator = 1.0f / 255.0f;
           List<Color> colorArray = new List<Color>();
           for (int i = imageBufferList.Count - 1; i >= 0; i -= stride)
           {
               float a = (int)(imageBufferList[i - 0]) * denominator;
               float r = (int)(imageBufferList[i - 1]) * denominator;
               float g = (int)(imageBufferList[i - 2]) * denominator;
               float b = (int)(imageBufferList[i - 3]) * denominator;

               colorArray.Add(new Color(r, g, b, a));
           }
           // Now we could do something with the array such as texture.SetPixels() or run image processing on the list
       }
       photoCaptureObject.StopPhotoModeAsync(OnStoppedPhotoMode);
   }
```

## <a name="video-capture"></a>Capture vidéo

**Namespace :** *UnityEngine.XR.WSA.WebCam*<br>
**Type :** *VideoCapture*

*VideoCapture* fonctionne de manière très similaire à *PhotoCapture*. Les seuls deux différences sont que vous devez spécifier une valeur de Frames par seconde (FPS) et vous pouvez uniquement enregistrer directement sur le disque en tant que fichier .mp4. Les étapes à utiliser *VideoCapture* sont les suivantes :
1. Créer un *VideoCapture* objet
2. Créer un *CameraParameters* objet avec les paramètres que nous voulons
3. Démarrer le Mode vidéo via *StartVideoModeAsync*
4. Démarrer l’enregistrement de vidéos
5. Arrêter l’enregistrement de vidéos
6. Arrêter le Mode de vidéo et nettoyer les ressources

Nous commençons par créer notre *VideoCapture* objet *VideoCapture m_VideoCapture = null ;*

```cs
void Start ()
   {
       VideoCapture.CreateAsync(false, OnVideoCaptureCreated);
   }
```

Nous allons ensuite configurer les paramètres que nous voulons pour l’enregistrement et le début.

```cs
void OnVideoCaptureCreated (VideoCapture videoCapture)
   {
       if (videoCapture != null)
       {
           m_VideoCapture = videoCapture;

           Resolution cameraResolution = VideoCapture.SupportedResolutions.OrderByDescending((res) => res.width * res.height).First();
           float cameraFramerate = VideoCapture.GetSupportedFrameRatesForResolution(cameraResolution).OrderByDescending((fps) => fps).First();

           CameraParameters cameraParameters = new CameraParameters();
           cameraParameters.hologramOpacity = 0.0f;
           cameraParameters.frameRate = cameraFramerate;
           cameraParameters.cameraResolutionWidth = cameraResolution.width;
           cameraParameters.cameraResolutionHeight = cameraResolution.height;
           cameraParameters.pixelFormat = CapturePixelFormat.BGRA32;

           m_VideoCapture.StartVideoModeAsync(cameraParameters,
                                               VideoCapture.AudioState.None,
                                               OnStartedVideoCaptureMode);
       }
       else
       {
           Debug.LogError("Failed to create VideoCapture Instance!");
       }
   }
```

Une fois démarré, nous allons commencer l’enregistrement

```cs
void OnStartedVideoCaptureMode(VideoCapture.VideoCaptureResult result)
   {
       if (result.success)
       {
           string filename = string.Format("MyVideo_{0}.mp4", Time.time);
           string filepath = System.IO.Path.Combine(Application.persistentDataPath, filename);

           m_VideoCapture.StartRecordingAsync(filepath, OnStartedRecordingVideo);
       }
   }
```

Une fois que l’enregistrement a démarré, vous pouvez mettre à jour votre interface utilisateur ou les comportements pour activer l’arrêt. Ici nous allons nous connecter simplement

```cs
void OnStartedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Started Recording Video!");
       // We will stop the video from recording via other input such as a timer or a tap, etc.
   }
```

À un moment ultérieur, nous souhaitons arrêter l’enregistrement. Cela peut se produire à partir d’une horloge ou une entrée utilisateur, par exemple.

```cs
// The user has indicated to stop recording
   void StopRecordingVideo()
   {
       m_VideoCapture.StopRecordingAsync(OnStoppedRecordingVideo);
   }
```

Une fois que l’enregistrement s’est arrêté, nous arrêterons mode vidéo et nettoyer à nos ressources.

```cs
void OnStoppedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Stopped Recording Video!");
       m_VideoCapture.StopVideoModeAsync(OnStoppedVideoCaptureMode);
   }

   void OnStoppedVideoCaptureMode(VideoCapture.VideoCaptureResult result)
   {
       m_VideoCapture.Dispose();
       m_VideoCapture = null;
   }
```

## <a name="troubleshooting"></a>Résolution des problèmes
* Aucune résolution n’est disponibles
    * Vérifiez le **WebCam** fonctionnalité est spécifiée dans votre projet.

## <a name="see-also"></a>Voir aussi
* [Appareil photo localisable](locatable-camera.md)
