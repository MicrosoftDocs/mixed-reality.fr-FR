---
title: Appareil photo localisable dans Unity
description: Utilisation de la caméra HoloLens localisable dans Unity.
author: wguyman
ms.author: wguyman
ms.date: 03/21/2018
ms.topic: article
keywords: photo, vidéo, hololens, appareil photo, Unity, localisable
ms.openlocfilehash: f0183400f55b1c6663a9a20ab4992befe5ad0718
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515437"
---
# <a name="locatable-camera-in-unity"></a>Appareil photo localisable dans Unity

## <a name="enabling-the-capability-for-photo-video-camera"></a>Activation de la fonctionnalité de Photo Video Camera

La fonctionnalité «WebCam» doit être déclarée pour qu’une application utilise l' [appareil photo](locatable-camera.md).
1. Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à la page «modifier les paramètres du projet > > Player».
2. Cliquer sur l’onglet «Windows Store»
3. Dans la section «fonctionnalités de > des paramètres de publication», vérifiez les fonctionnalités de la **webcam** et du **microphone**

Une seule opération peut être effectuée avec la caméra à la fois. Pour déterminer le mode (photo, vidéo ou aucun) dans lequel se trouve actuellement l’appareil photo, vous pouvez vérifier UnityEngine. XR. WSA. WebCam. mode.

## <a name="photo-capture"></a>Capture de photos

**Espace de noms :** *UnityEngine. XR. WSA. WebCam*<br>
**Type :** *PhotoCapture*

Le  type PhotoCapture vous permet de prendre des photographies avec la caméra photo. Le modèle général d’utilisation  de PhotoCapture pour prendre une photo est le suivant:
1. Créer un  objet PhotoCapture
2. Créer un objet *CameraParameters* avec les paramètres de votre choix
3. Démarrer le mode photo via *StartPhotoModeAsync*
4. Prenez la photo souhaitée
    * facultatif Interagir avec cette image
5. Arrêter le mode photo et nettoyer les ressources

### <a name="common-set-up-for-photocapture"></a>Configuration commune pour la PhotoCapture

Pour les trois utilisations, nous commençons par les trois premières étapes ci-dessus.

Nous commençons par créer  un objet PhotoCapture

```cs
PhotoCapture photoCaptureObject = null;
   void Start()
   {
       PhotoCapture.CreateAsync(false, OnPhotoCaptureCreated);
   }
```

Ensuite, nous stockons notre objet, définissons les paramètres et commençons le mode photo

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

Au final, nous utiliserons également le même code de nettoyage présenté ici

```cs
void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
   {
       photoCaptureObject.Dispose();
       photoCaptureObject = null;
   }
```

Après ces étapes, vous pouvez choisir le type de photo à capturer.

### <a name="capture-a-photo-to-a-file"></a>Capturer une photo dans un fichier

L’opération la plus simple consiste à capturer directement une photo dans un fichier. La photo peut être enregistrée au format JPG ou PNG.

Si nous avons correctement démarré le mode photo, nous allons maintenant prendre une photo et la stocker sur le disque

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

Une fois que vous avez capturé la photo sur le disque, nous allons quitter le mode photo, puis nettoyer nos objets

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

### <a name="capture-a-photo-to-a-texture2d"></a>Capturer une photo sur un Texture2D

Lors de la capture de données dans un Texture2D, le processus est très similaire à la capture sur le disque.

Nous suivrons le processus de configuration ci-dessus.

Dans *OnPhotoModeStarted*, nous capturerons un frame en mémoire.

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

Nous allons ensuite appliquer notre résultat à une texture et utiliser le code de nettoyage commun ci-dessus.

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

### <a name="capture-a-photo-and-interact-with-the-raw-bytes"></a>Capturer une photo et interagir avec les octets bruts

Pour interagir avec les octets bruts d’un en mémoire, nous suivons les mêmes étapes que ci-dessus et *OnPhotoModeStarted* comme pour la capture d’une photo à un Texture2D. La différence réside dans *OnCapturedPhotoToMemory* où nous pouvons récupérer les octets bruts et interagir avec eux.

Dans cet exemple, nous allons créer une *liste<Color>*  qui peut être traitée ultérieurement ou appliquée à une texture par le biais de *setPixels ()*

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

**Espace de noms :** *UnityEngine. XR. WSA. WebCam*<br>
**Type :** *VideoCapture*

*VideoCapture* fonctionne de façon très similaire à la PhotoCapture. Les deux seules différences sont que vous devez spécifier une valeur d’images par seconde (FPS) et vous ne pouvez enregistrer directement sur le disque qu’en tant que fichier. MP4. Les étapes d’utilisation de *VideoCapture* sont les suivantes:
1. Créer un objet *VideoCapture*
2. Créer un objet *CameraParameters* avec les paramètres de votre choix
3. Démarrer le mode vidéo via *StartVideoModeAsync*
4. Démarrer l’enregistrement vidéo
5. Arrêter l’enregistrement de la vidéo
6. Arrêter le mode vidéo et nettoyer les ressources

Nous commençons par créer notre objet *VideoCapture* *VideoCapture m_VideoCapture = null;*

```cs
void Start ()
   {
       VideoCapture.CreateAsync(false, OnVideoCaptureCreated);
   }
```

Nous allons ensuite configurer les paramètres à utiliser pour l’enregistrement et démarrer.

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

Une fois démarré, nous commençons l’enregistrement

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

Une fois l’enregistrement démarré, vous pouvez mettre à jour votre interface utilisateur ou les comportements pour activer l’arrêt. Ici, nous allons simplement nous connecter

```cs
void OnStartedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Started Recording Video!");
       // We will stop the video from recording via other input such as a timer or a tap, etc.
   }
```

À un moment ultérieur, nous voulons arrêter l’enregistrement. Cela peut se produire à partir d’une entrée d’horloge ou d’utilisateur, par exemple.

```cs
// The user has indicated to stop recording
   void StopRecordingVideo()
   {
       m_VideoCapture.StopRecordingAsync(OnStoppedRecordingVideo);
   }
```

Une fois que l’enregistrement s’est arrêté, nous allons arrêter le mode vidéo et nettoyer nos ressources.

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
* Aucune résolution n’est disponible
    * Assurez-vous que la fonctionnalité **webcam** est spécifiée dans votre projet.

## <a name="see-also"></a>Voir aussi
* [Appareil photo localisable](locatable-camera.md)
