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
# <a name="locatable-camera-in-unity"></a><span data-ttu-id="49179-104">Caméra localisable dans Unity</span><span class="sxs-lookup"><span data-stu-id="49179-104">Locatable camera in Unity</span></span>

## <a name="enabling-the-capability-for-photo-video-camera"></a><span data-ttu-id="49179-105">L’activation de la fonctionnalité pour la caméra vidéo Photo</span><span class="sxs-lookup"><span data-stu-id="49179-105">Enabling the capability for Photo Video Camera</span></span>

<span data-ttu-id="49179-106">La fonctionnalité « WebCam » doit être déclarée pour une application d’utiliser le [caméra](locatable-camera.md).</span><span class="sxs-lookup"><span data-stu-id="49179-106">The "WebCam" capability must be declared for an app to use the [camera](locatable-camera.md).</span></span>
1. <span data-ttu-id="49179-107">Dans l’éditeur Unity, accédez aux paramètres de lecteur en accédant à la page « Modifier > projet Paramètres > lecteur »</span><span class="sxs-lookup"><span data-stu-id="49179-107">In the Unity Editor, go to the player settings by navigating to "Edit > Project Settings > Player" page</span></span>
2. <span data-ttu-id="49179-108">Cliquez sur l’onglet « Windows Store »</span><span class="sxs-lookup"><span data-stu-id="49179-108">Click on the "Windows Store" tab</span></span>
3. <span data-ttu-id="49179-109">Dans la section « Paramètres > des fonctionnalités de publication », vérifiez le **WebCam** et **Microphone** fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="49179-109">In the "Publishing Settings > Capabilities" section, check the **WebCam** and **Microphone** capabilities</span></span>

<span data-ttu-id="49179-110">Seule une opération peut se produire avec l’appareil photo à la fois.</span><span class="sxs-lookup"><span data-stu-id="49179-110">Only a single operation can occur with the camera at a time.</span></span> <span data-ttu-id="49179-111">Pour déterminer quel mode (photos, vidéo ou aucun) la caméra en cours, vous pouvez vérifier UnityEngine.XR.WSA.WebCam.Mode.</span><span class="sxs-lookup"><span data-stu-id="49179-111">To determine which mode (photo, video, or none) the camera is currently in, you can check UnityEngine.XR.WSA.WebCam.Mode.</span></span>

## <a name="photo-capture"></a><span data-ttu-id="49179-112">Capture de photos</span><span class="sxs-lookup"><span data-stu-id="49179-112">Photo Capture</span></span>

<span data-ttu-id="49179-113">**Namespace :** *UnityEngine.XR.WSA.WebCam*</span><span class="sxs-lookup"><span data-stu-id="49179-113">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="49179-114">**Type :** *PhotoCapture*</span><span class="sxs-lookup"><span data-stu-id="49179-114">**Type:** *PhotoCapture*</span></span>

<span data-ttu-id="49179-115">Le *PhotoCapture* type vous permet de prendre encore photographies avec la caméra vidéo Photo.</span><span class="sxs-lookup"><span data-stu-id="49179-115">The *PhotoCapture* type allows you to take still photographs with the Photo Video Camera.</span></span> <span data-ttu-id="49179-116">Le modèle général pour l’utilisation de *PhotoCapture* à prendre une photo est comme suit :</span><span class="sxs-lookup"><span data-stu-id="49179-116">The general pattern for using *PhotoCapture* to take a photo is as follows:</span></span>
1. <span data-ttu-id="49179-117">Créer un *PhotoCapture* objet</span><span class="sxs-lookup"><span data-stu-id="49179-117">Create a *PhotoCapture* object</span></span>
2. <span data-ttu-id="49179-118">Créer un *CameraParameters* objet avec les paramètres que nous voulons</span><span class="sxs-lookup"><span data-stu-id="49179-118">Create a *CameraParameters* object with the settings we want</span></span>
3. <span data-ttu-id="49179-119">Démarrer le Mode de Photo via *StartPhotoModeAsync*</span><span class="sxs-lookup"><span data-stu-id="49179-119">Start Photo Mode via *StartPhotoModeAsync*</span></span>
4. <span data-ttu-id="49179-120">Prendre la photo</span><span class="sxs-lookup"><span data-stu-id="49179-120">Take the desired photo</span></span>
    * <span data-ttu-id="49179-121">(facultatif) Interagir avec cette image</span><span class="sxs-lookup"><span data-stu-id="49179-121">(optional) Interact with that picture</span></span>
5. <span data-ttu-id="49179-122">Arrêter le Mode de Photo et de nettoyer les ressources</span><span class="sxs-lookup"><span data-stu-id="49179-122">Stop Photo Mode and clean up resources</span></span>

### <a name="common-set-up-for-photocapture"></a><span data-ttu-id="49179-123">Ensemble commun de pour PhotoCapture</span><span class="sxs-lookup"><span data-stu-id="49179-123">Common Set Up for PhotoCapture</span></span>

<span data-ttu-id="49179-124">Pour toutes les utilisations de trois, nous commençons avec le même 3 premières étapes ci-dessus</span><span class="sxs-lookup"><span data-stu-id="49179-124">For all three uses, we start with the same first 3 steps above</span></span>

<span data-ttu-id="49179-125">Nous commençons par créer un *PhotoCapture* objet</span><span class="sxs-lookup"><span data-stu-id="49179-125">We start by creating a *PhotoCapture* object</span></span>

```cs
PhotoCapture photoCaptureObject = null;
   void Start()
   {
       PhotoCapture.CreateAsync(false, OnPhotoCaptureCreated);
   }
```

<span data-ttu-id="49179-126">Ensuite nous stocker notre objet défini nos paramètres et démarrer le Mode de la Photo</span><span class="sxs-lookup"><span data-stu-id="49179-126">Next we store our object, set our parameters, and start Photo Mode</span></span>

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

<span data-ttu-id="49179-127">Au final, nous utiliserons également le même code présenté ici de nettoyage</span><span class="sxs-lookup"><span data-stu-id="49179-127">In the end, we will also use the same clean up code presented here</span></span>

```cs
void OnStoppedPhotoMode(PhotoCapture.PhotoCaptureResult result)
   {
       photoCaptureObject.Dispose();
       photoCaptureObject = null;
   }
```

<span data-ttu-id="49179-128">Une fois ces étapes effectuées, vous pouvez choisir le type de la photo pour capturer.</span><span class="sxs-lookup"><span data-stu-id="49179-128">After these steps, you can choose which type of photo to capture.</span></span>

### <a name="capture-a-photo-to-a-file"></a><span data-ttu-id="49179-129">Capturer une Photo dans un fichier</span><span class="sxs-lookup"><span data-stu-id="49179-129">Capture a Photo to a File</span></span>

<span data-ttu-id="49179-130">L’opération la plus simple consiste à capturer une photo directement dans un fichier.</span><span class="sxs-lookup"><span data-stu-id="49179-130">The simplest operation is to capture a photo directly to a file.</span></span> <span data-ttu-id="49179-131">La photo peut être enregistrée comme un fichier JPG ou PNG.</span><span class="sxs-lookup"><span data-stu-id="49179-131">The photo can be saved as a JPG or a PNG.</span></span>

<span data-ttu-id="49179-132">Si nous avons commencé avec succès mode photo, nous maintenant prendre une photo et stockez-le sur le disque</span><span class="sxs-lookup"><span data-stu-id="49179-132">If we successfully started photo mode, we now will take a photo and store it on disk</span></span>

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

<span data-ttu-id="49179-133">Après avoir capturé la photo sur le disque, nous quitter le mode de photo et puis nettoyer nos objets</span><span class="sxs-lookup"><span data-stu-id="49179-133">After capturing the photo to disk, we will exit photo mode and then clean up our objects</span></span>

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

### <a name="capture-a-photo-to-a-texture2d"></a><span data-ttu-id="49179-134">Capturer une Photo à une Texture2D</span><span class="sxs-lookup"><span data-stu-id="49179-134">Capture a Photo to a Texture2D</span></span>

<span data-ttu-id="49179-135">Lors de la capture des données à une Texture2D, le processus est très similaire à la capture sur le disque.</span><span class="sxs-lookup"><span data-stu-id="49179-135">When capturing data to a Texture2D, the process is extremely similar to capturing to disk.</span></span>

<span data-ttu-id="49179-136">Nous allons suivre l’ensemble des processus ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="49179-136">We will follow the set up process above.</span></span>

<span data-ttu-id="49179-137">Dans *OnPhotoModeStarted*, nous sera capturer un frame dans la mémoire.</span><span class="sxs-lookup"><span data-stu-id="49179-137">In *OnPhotoModeStarted*, we will capture a frame to memory.</span></span>

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

<span data-ttu-id="49179-138">Puis nous appliquer nos résultats à une texture et utiliserons courantes nettoyer le code ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="49179-138">We will then apply our result to a texture and use the common clean up code above.</span></span>

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

### <a name="capture-a-photo-and-interact-with-the-raw-bytes"></a><span data-ttu-id="49179-139">Capturer une Photo et l’interaction avec les octets bruts</span><span class="sxs-lookup"><span data-stu-id="49179-139">Capture a Photo and Interact with the Raw bytes</span></span>

<span data-ttu-id="49179-140">Pour interagir avec les octets bruts d’une mémoire frame, nous allons suivre les mêmes étapes que ci-dessus et *OnPhotoModeStarted* comme dans la capture d’une photo à une Texture2D.</span><span class="sxs-lookup"><span data-stu-id="49179-140">To interact with the raw bytes of an in memory frame, we will follow the same set up steps as above and *OnPhotoModeStarted* as in capturing a photo to a Texture2D.</span></span> <span data-ttu-id="49179-141">La différence réside dans *OnCapturedPhotoToMemory* où nous pouvons obtenir les octets bruts et interagir avec eux.</span><span class="sxs-lookup"><span data-stu-id="49179-141">The difference is in *OnCapturedPhotoToMemory* where we can get the raw bytes and interact with them.</span></span>

<span data-ttu-id="49179-142">Dans cet exemple, nous allons créer un *liste<Color>*  qui pourrait être plu traité ou appliqués à une texture via *SetPixels()*</span><span class="sxs-lookup"><span data-stu-id="49179-142">In this example, we will create a *List<Color>* which could be further processed or applied to a texture via *SetPixels()*</span></span>

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

## <a name="video-capture"></a><span data-ttu-id="49179-143">Capture vidéo</span><span class="sxs-lookup"><span data-stu-id="49179-143">Video Capture</span></span>

<span data-ttu-id="49179-144">**Namespace :** *UnityEngine.XR.WSA.WebCam*</span><span class="sxs-lookup"><span data-stu-id="49179-144">**Namespace:** *UnityEngine.XR.WSA.WebCam*</span></span><br>
<span data-ttu-id="49179-145">**Type :** *VideoCapture*</span><span class="sxs-lookup"><span data-stu-id="49179-145">**Type:** *VideoCapture*</span></span>

<span data-ttu-id="49179-146">*VideoCapture* fonctionne de manière très similaire à *PhotoCapture*.</span><span class="sxs-lookup"><span data-stu-id="49179-146">*VideoCapture* functions very similarly to *PhotoCapture*.</span></span> <span data-ttu-id="49179-147">Les seuls deux différences sont que vous devez spécifier une valeur de Frames par seconde (FPS) et vous pouvez uniquement enregistrer directement sur le disque en tant que fichier .mp4.</span><span class="sxs-lookup"><span data-stu-id="49179-147">The only two differences are that you must specify a Frames Per Second (FPS) value and you can only save directly to disk as an .mp4 file.</span></span> <span data-ttu-id="49179-148">Les étapes à utiliser *VideoCapture* sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="49179-148">The steps to use *VideoCapture* are as follows:</span></span>
1. <span data-ttu-id="49179-149">Créer un *VideoCapture* objet</span><span class="sxs-lookup"><span data-stu-id="49179-149">Create a *VideoCapture* object</span></span>
2. <span data-ttu-id="49179-150">Créer un *CameraParameters* objet avec les paramètres que nous voulons</span><span class="sxs-lookup"><span data-stu-id="49179-150">Create a *CameraParameters* object with the settings we want</span></span>
3. <span data-ttu-id="49179-151">Démarrer le Mode vidéo via *StartVideoModeAsync*</span><span class="sxs-lookup"><span data-stu-id="49179-151">Start Video Mode via *StartVideoModeAsync*</span></span>
4. <span data-ttu-id="49179-152">Démarrer l’enregistrement de vidéos</span><span class="sxs-lookup"><span data-stu-id="49179-152">Start recording video</span></span>
5. <span data-ttu-id="49179-153">Arrêter l’enregistrement de vidéos</span><span class="sxs-lookup"><span data-stu-id="49179-153">Stop recording video</span></span>
6. <span data-ttu-id="49179-154">Arrêter le Mode de vidéo et nettoyer les ressources</span><span class="sxs-lookup"><span data-stu-id="49179-154">Stop Video Mode and clean up resources</span></span>

<span data-ttu-id="49179-155">Nous commençons par créer notre *VideoCapture* objet *VideoCapture m_VideoCapture = null ;*</span><span class="sxs-lookup"><span data-stu-id="49179-155">We start by creating our *VideoCapture* object *VideoCapture m_VideoCapture = null;*</span></span>

```cs
void Start ()
   {
       VideoCapture.CreateAsync(false, OnVideoCaptureCreated);
   }
```

<span data-ttu-id="49179-156">Nous allons ensuite configurer les paramètres que nous voulons pour l’enregistrement et le début.</span><span class="sxs-lookup"><span data-stu-id="49179-156">We then will set up the parameters we will want for the recording and start.</span></span>

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

<span data-ttu-id="49179-157">Une fois démarré, nous allons commencer l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="49179-157">Once started, we will begin the recording</span></span>

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

<span data-ttu-id="49179-158">Une fois que l’enregistrement a démarré, vous pouvez mettre à jour votre interface utilisateur ou les comportements pour activer l’arrêt.</span><span class="sxs-lookup"><span data-stu-id="49179-158">After recording has started, you could update your UI or behaviors to enable stopping.</span></span> <span data-ttu-id="49179-159">Ici nous allons nous connecter simplement</span><span class="sxs-lookup"><span data-stu-id="49179-159">Here we just log</span></span>

```cs
void OnStartedRecordingVideo(VideoCapture.VideoCaptureResult result)
   {
       Debug.Log("Started Recording Video!");
       // We will stop the video from recording via other input such as a timer or a tap, etc.
   }
```

<span data-ttu-id="49179-160">À un moment ultérieur, nous souhaitons arrêter l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="49179-160">At a later point, we will want to stop the recording.</span></span> <span data-ttu-id="49179-161">Cela peut se produire à partir d’une horloge ou une entrée utilisateur, par exemple.</span><span class="sxs-lookup"><span data-stu-id="49179-161">This could happen from a timer or user input, for instance.</span></span>

```cs
// The user has indicated to stop recording
   void StopRecordingVideo()
   {
       m_VideoCapture.StopRecordingAsync(OnStoppedRecordingVideo);
   }
```

<span data-ttu-id="49179-162">Une fois que l’enregistrement s’est arrêté, nous arrêterons mode vidéo et nettoyer à nos ressources.</span><span class="sxs-lookup"><span data-stu-id="49179-162">Once the recording has stopped, we will stop video mode and clean up our resources.</span></span>

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

## <a name="troubleshooting"></a><span data-ttu-id="49179-163">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="49179-163">Troubleshooting</span></span>
* <span data-ttu-id="49179-164">Aucune résolution n’est disponibles</span><span class="sxs-lookup"><span data-stu-id="49179-164">No resolutions are available</span></span>
    * <span data-ttu-id="49179-165">Vérifiez le **WebCam** fonctionnalité est spécifiée dans votre projet.</span><span class="sxs-lookup"><span data-stu-id="49179-165">Ensure the **WebCam** capability is specified in your project.</span></span>

## <a name="see-also"></a><span data-ttu-id="49179-166">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="49179-166">See Also</span></span>
* [<span data-ttu-id="49179-167">Appareil photo localisable</span><span class="sxs-lookup"><span data-stu-id="49179-167">Locatable camera</span></span>](locatable-camera.md)
