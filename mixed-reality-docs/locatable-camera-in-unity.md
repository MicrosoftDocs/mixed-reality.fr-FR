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
# <a name="locatable-camera-in-unity"></a><span data-ttu-id="4834f-104">Appareil photo localisable dans Unity</span><span class="sxs-lookup"><span data-stu-id="4834f-104">Locatable camera in Unity</span></span>

## <a name="enabling-the-capability-for-photo-video-camera"></a><span data-ttu-id="4834f-105">Activation de la fonctionnalité de Photo Video Camera</span><span class="sxs-lookup"><span data-stu-id="4834f-105">Enabling the capability for Photo Video Camera</span></span>

<span data-ttu-id="4834f-106">La fonctionnalité «WebCam» doit être déclarée pour qu’une application utilise l' [appareil photo](locatable-camera.md).</span><span class="sxs-lookup"><span data-stu-id="4834f-106">The "WebCam" capability must be declared for an app to use the [camera](locatable-camera.md).</span></span>
1. <span data-ttu-id="4834f-107">Dans l’éditeur Unity, accédez aux paramètres du lecteur en accédant à la page «modifier les paramètres du projet > > Player».</span><span class="sxs-lookup"><span data-stu-id="4834f-107">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player" page</span></span>
2. <span data-ttu-id="4834f-108">Cliquer sur l’onglet «Windows Store»</span><span class="sxs-lookup"><span data-stu-id="4834f-108">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="4834f-109">Dans la section «fonctionnalités de > des paramètres de publication», vérifiez les fonctionnalités de la **webcam** et du **microphone**</span><span class="sxs-lookup"><span data-stu-id="4834f-109">In the "Publishing Settings > Capabilities" section, check the **WebCam** and **Microphone** capabilities</span></span>

<span data-ttu-id="4834f-110">Une seule opération peut être effectuée avec la caméra à la fois.</span><span class="sxs-lookup"><span data-stu-id="4834f-110">Only a single operation can occur with the camera at a time.</span></span> <span data-ttu-id="4834f-111">Pour déterminer le mode (photo, vidéo ou aucun) dans lequel se trouve actuellement l’appareil photo, vous pouvez vérifier UnityEngine. XR. WSA. WebCam. mode.</span><span class="sxs-lookup"><span data-stu-id="4834f-111">To determine which mode (photo, video, or none) the camera is currently in, you can check UnityEngine.XR.WSA.WebCam.Mode.</span></span>

## <a name="photo-capture"></a><span data-ttu-id="4834f-112">Capture de photos</span><span class="sxs-lookup"><span data-stu-id="4834f-112">Photo Capture</span></span>

<span data-ttu-id="4834f-113">**Espace de noms :** *UnityEngine. XR. WSA. WebCam*</span><span class="sxs-lookup"><span data-stu-id="4834f-113">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="4834f-114">**Type :** *PhotoCapture*</span><span class="sxs-lookup"><span data-stu-id="4834f-114">**Type:** *PhotoCapture*</span></span>

<span data-ttu-id="4834f-115">Le  type PhotoCapture vous permet de prendre des photographies avec la caméra photo.</span><span class="sxs-lookup"><span data-stu-id="4834f-115">The *PhotoCapture* type allows you to take still photographs with the Photo Video Camera.</span></span> <span data-ttu-id="4834f-116">Le modèle général d’utilisation  de PhotoCapture pour prendre une photo est le suivant:</span><span class="sxs-lookup"><span data-stu-id="4834f-116">The general pattern for using *PhotoCapture* to take a photo is as follows:</span></span>
1. <span data-ttu-id="4834f-117">Créer un  objet PhotoCapture</span><span class="sxs-lookup"><span data-stu-id="4834f-117">Create a *PhotoCapture* object</span></span>
2. <span data-ttu-id="4834f-118">Créer un objet *CameraParameters* avec les paramètres de votre choix</span><span class="sxs-lookup"><span data-stu-id="4834f-118">Create a *CameraParameters* object with the settings we want</span></span>
3. <span data-ttu-id="4834f-119">Démarrer le mode photo via *StartPhotoModeAsync*</span><span class="sxs-lookup"><span data-stu-id="4834f-119">Start Photo Mode via *StartPhotoModeAsync*</span></span>
4. <span data-ttu-id="4834f-120">Prenez la photo souhaitée</span><span class="sxs-lookup"><span data-stu-id="4834f-120">Take the desired photo</span></span>
    * <span data-ttu-id="4834f-121">facultatif Interagir avec cette image</span><span class="sxs-lookup"><span data-stu-id="4834f-121">(optional) Interact with that picture</span></span>
5. <span data-ttu-id="4834f-122">Arrêter le mode photo et nettoyer les ressources</span><span class="sxs-lookup"><span data-stu-id="4834f-122">Stop Photo Mode and clean up resources</span></span>

### <a name="common-set-up-for-photocapture"></a><span data-ttu-id="4834f-123">Configuration commune pour la PhotoCapture</span><span class="sxs-lookup"><span data-stu-id="4834f-123">Common Set Up for PhotoCapture</span></span>

<span data-ttu-id="4834f-124">Pour les trois utilisations, nous commençons par les trois premières étapes ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4834f-124">For all three uses, we start with the same first 3 steps above</span></span>

<span data-ttu-id="4834f-125">Nous commençons par créer  un objet PhotoCapture</span><span class="sxs-lookup"><span data-stu-id="4834f-125">We start by creating a *PhotoCapture* object</span></span>

```cs
PhotoCapture photoCaptureObject = null;
   void Start()
   {
       PhotoCapture.CreateAsync(false, OnPhotoCaptureCreated);
   }
```

<span data-ttu-id="4834f-126">Ensuite, nous stockons notre objet, définissons les paramètres et commençons le mode photo</span><span class="sxs-lookup"><span data-stu-id="4834f-126">Next we store our object, set our parameters, and start Photo Mode</span></span>

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

<span data-ttu-id="4834f-127">Au final, nous utiliserons également le même code de nettoyage présenté ici</span><span class="sxs-lookup"><span data-stu-id="4834f-127">In the end, we will also use the same clean up code presented here</span></span>

```cs
void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
   {
       photoCaptureObject.Dispose();
       photoCaptureObject = null;
   }
```

<span data-ttu-id="4834f-128">Après ces étapes, vous pouvez choisir le type de photo à capturer.</span><span class="sxs-lookup"><span data-stu-id="4834f-128">After these steps, you can choose which type of photo to capture.</span></span>

### <a name="capture-a-photo-to-a-file"></a><span data-ttu-id="4834f-129">Capturer une photo dans un fichier</span><span class="sxs-lookup"><span data-stu-id="4834f-129">Capture a Photo to a File</span></span>

<span data-ttu-id="4834f-130">L’opération la plus simple consiste à capturer directement une photo dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="4834f-130">The simplest operation is to capture a photo directly to a file.</span></span> <span data-ttu-id="4834f-131">La photo peut être enregistrée au format JPG ou PNG.</span><span class="sxs-lookup"><span data-stu-id="4834f-131">The photo can be saved as a JPG or a PNG.</span></span>

<span data-ttu-id="4834f-132">Si nous avons correctement démarré le mode photo, nous allons maintenant prendre une photo et la stocker sur le disque</span><span class="sxs-lookup"><span data-stu-id="4834f-132">If we successfully started photo mode, we now will take a photo and store it on disk</span></span>

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

<span data-ttu-id="4834f-133">Une fois que vous avez capturé la photo sur le disque, nous allons quitter le mode photo, puis nettoyer nos objets</span><span class="sxs-lookup"><span data-stu-id="4834f-133">After capturing the photo to disk, we will exit photo mode and then clean up our objects</span></span>

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

### <a name="capture-a-photo-to-a-texture2d"></a><span data-ttu-id="4834f-134">Capturer une photo sur un Texture2D</span><span class="sxs-lookup"><span data-stu-id="4834f-134">Capture a Photo to a Texture2D</span></span>

<span data-ttu-id="4834f-135">Lors de la capture de données dans un Texture2D, le processus est très similaire à la capture sur le disque.</span><span class="sxs-lookup"><span data-stu-id="4834f-135">When capturing data to a Texture2D, the process is extremely similar to capturing to disk.</span></span>

<span data-ttu-id="4834f-136">Nous suivrons le processus de configuration ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4834f-136">We will follow the set up process above.</span></span>

<span data-ttu-id="4834f-137">Dans *OnPhotoModeStarted*, nous capturerons un frame en mémoire.</span><span class="sxs-lookup"><span data-stu-id="4834f-137">In *OnPhotoModeStarted*, we will capture a frame to memory.</span></span>

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

<span data-ttu-id="4834f-138">Nous allons ensuite appliquer notre résultat à une texture et utiliser le code de nettoyage commun ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="4834f-138">We will then apply our result to a texture and use the common clean up code above.</span></span>

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

### <a name="capture-a-photo-and-interact-with-the-raw-bytes"></a><span data-ttu-id="4834f-139">Capturer une photo et interagir avec les octets bruts</span><span class="sxs-lookup"><span data-stu-id="4834f-139">Capture a Photo and Interact with the Raw bytes</span></span>

<span data-ttu-id="4834f-140">Pour interagir avec les octets bruts d’un en mémoire, nous suivons les mêmes étapes que ci-dessus et *OnPhotoModeStarted* comme pour la capture d’une photo à un Texture2D.</span><span class="sxs-lookup"><span data-stu-id="4834f-140">To interact with the raw bytes of an in memory frame, we will follow the same set up steps as above and *OnPhotoModeStarted* as in capturing a photo to a Texture2D.</span></span> <span data-ttu-id="4834f-141">La différence réside dans *OnCapturedPhotoToMemory* où nous pouvons récupérer les octets bruts et interagir avec eux.</span><span class="sxs-lookup"><span data-stu-id="4834f-141">The difference is in *OnCapturedPhotoToMemory* where we can get the raw bytes and interact with them.</span></span>

<span data-ttu-id="4834f-142">Dans cet exemple, nous allons créer une *liste<Color>*  qui peut être traitée ultérieurement ou appliquée à une texture par le biais de *setPixels ()*</span><span class="sxs-lookup"><span data-stu-id="4834f-142">In this example, we will create a *List<Color>* which could be further processed or applied to a texture via *SetPixels()*</span></span>

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

## <a name="video-capture"></a><span data-ttu-id="4834f-143">Capture vidéo</span><span class="sxs-lookup"><span data-stu-id="4834f-143">Video Capture</span></span>

<span data-ttu-id="4834f-144">**Espace de noms :** *UnityEngine. XR. WSA. WebCam*</span><span class="sxs-lookup"><span data-stu-id="4834f-144">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="4834f-145">**Type :** *VideoCapture*</span><span class="sxs-lookup"><span data-stu-id="4834f-145">**Type:** *VideoCapture*</span></span>

<span data-ttu-id="4834f-146">*VideoCapture* fonctionne de façon très similaire à la PhotoCapture.</span><span class="sxs-lookup"><span data-stu-id="4834f-146">*VideoCapture* functions very similarly to *PhotoCapture*.</span></span> <span data-ttu-id="4834f-147">Les deux seules différences sont que vous devez spécifier une valeur d’images par seconde (FPS) et vous ne pouvez enregistrer directement sur le disque qu’en tant que fichier. MP4.</span><span class="sxs-lookup"><span data-stu-id="4834f-147">The only two differences are that you must specify a Frames Per Second (FPS) value and you can only save directly to disk as an .mp4 file.</span></span> <span data-ttu-id="4834f-148">Les étapes d’utilisation de *VideoCapture* sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="4834f-148">The steps to use *VideoCapture* are as follows:</span></span>
1. <span data-ttu-id="4834f-149">Créer un objet *VideoCapture*</span><span class="sxs-lookup"><span data-stu-id="4834f-149">Create a *VideoCapture* object</span></span>
2. <span data-ttu-id="4834f-150">Créer un objet *CameraParameters* avec les paramètres de votre choix</span><span class="sxs-lookup"><span data-stu-id="4834f-150">Create a *CameraParameters* object with the settings we want</span></span>
3. <span data-ttu-id="4834f-151">Démarrer le mode vidéo via *StartVideoModeAsync*</span><span class="sxs-lookup"><span data-stu-id="4834f-151">Start Video Mode via *StartVideoModeAsync*</span></span>
4. <span data-ttu-id="4834f-152">Démarrer l’enregistrement vidéo</span><span class="sxs-lookup"><span data-stu-id="4834f-152">Start recording video</span></span>
5. <span data-ttu-id="4834f-153">Arrêter l’enregistrement de la vidéo</span><span class="sxs-lookup"><span data-stu-id="4834f-153">Stop recording video</span></span>
6. <span data-ttu-id="4834f-154">Arrêter le mode vidéo et nettoyer les ressources</span><span class="sxs-lookup"><span data-stu-id="4834f-154">Stop Video Mode and clean up resources</span></span>

<span data-ttu-id="4834f-155">Nous commençons par créer notre objet *VideoCapture* *VideoCapture m_VideoCapture = null;*</span><span class="sxs-lookup"><span data-stu-id="4834f-155">We start by creating our *VideoCapture* object *VideoCapture m_VideoCapture = null;*</span></span>

```cs
void Start ()
   {
       VideoCapture.CreateAsync(false, OnVideoCaptureCreated);
   }
```

<span data-ttu-id="4834f-156">Nous allons ensuite configurer les paramètres à utiliser pour l’enregistrement et démarrer.</span><span class="sxs-lookup"><span data-stu-id="4834f-156">We then will set up the parameters we will want for the recording and start.</span></span>

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

<span data-ttu-id="4834f-157">Une fois démarré, nous commençons l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="4834f-157">Once started, we will begin the recording</span></span>

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

<span data-ttu-id="4834f-158">Une fois l’enregistrement démarré, vous pouvez mettre à jour votre interface utilisateur ou les comportements pour activer l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="4834f-158">After recording has started, you could update your UI or behaviors to enable stopping.</span></span> <span data-ttu-id="4834f-159">Ici, nous allons simplement nous connecter</span><span class="sxs-lookup"><span data-stu-id="4834f-159">Here we just log</span></span>

```cs
void OnStartedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Started Recording Video!");
       // We will stop the video from recording via other input such as a timer or a tap, etc.
   }
```

<span data-ttu-id="4834f-160">À un moment ultérieur, nous voulons arrêter l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="4834f-160">At a later point, we will want to stop the recording.</span></span> <span data-ttu-id="4834f-161">Cela peut se produire à partir d’une entrée d’horloge ou d’utilisateur, par exemple.</span><span class="sxs-lookup"><span data-stu-id="4834f-161">This could happen from a timer or user input, for instance.</span></span>

```cs
// The user has indicated to stop recording
   void StopRecordingVideo()
   {
       m_VideoCapture.StopRecordingAsync(OnStoppedRecordingVideo);
   }
```

<span data-ttu-id="4834f-162">Une fois que l’enregistrement s’est arrêté, nous allons arrêter le mode vidéo et nettoyer nos ressources.</span><span class="sxs-lookup"><span data-stu-id="4834f-162">Once the recording has stopped, we will stop video mode and clean up our resources.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="4834f-163">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="4834f-163">Troubleshooting</span></span>
* <span data-ttu-id="4834f-164">Aucune résolution n’est disponible</span><span class="sxs-lookup"><span data-stu-id="4834f-164">No resolutions are available</span></span>
    * <span data-ttu-id="4834f-165">Assurez-vous que la fonctionnalité **webcam** est spécifiée dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="4834f-165">Ensure the **WebCam** capability is specified in your project.</span></span>

## <a name="see-also"></a><span data-ttu-id="4834f-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="4834f-166">See Also</span></span>
* [<span data-ttu-id="4834f-167">Appareil photo localisable</span><span class="sxs-lookup"><span data-stu-id="4834f-167">Locatable camera</span></span>](locatable-camera.md)
