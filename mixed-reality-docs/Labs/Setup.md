# <a name="setting-up"></a><span data-ttu-id="ad8f5-101">Configuration de</span><span class="sxs-lookup"><span data-stu-id="ad8f5-101">Setting Up</span></span>

<span data-ttu-id="ad8f5-102">Mise en route avec l’API de DK Kinect Azure ?</span><span class="sxs-lookup"><span data-stu-id="ad8f5-102">Getting started with the Azure Kinect DK API?</span></span> <span data-ttu-id="ad8f5-103">Ne cherchez plus !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-103">Look no further!</span></span> <span data-ttu-id="ad8f5-104">Ce document vous aidera à en cours d’exécution avec un accès à l’appareil !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-104">This document will get you up and running with access to the device!</span></span>

<span data-ttu-id="ad8f5-105">Tout d’abord, téléchargez et installez le [Azure Kinect DK API](https://github.com/Microsoft/Azure-Kinect-Sensor-SDK) à partir de Github.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-105">First, download and install the [Azure Kinect DK API](https://github.com/Microsoft/Azure-Kinect-Sensor-SDK) from Github.</span></span>

<span data-ttu-id="ad8f5-106">**Contenu**</span><span class="sxs-lookup"><span data-stu-id="ad8f5-106">**Contents**</span></span>  
[<span data-ttu-id="ad8f5-107">En-têtes</span><span class="sxs-lookup"><span data-stu-id="ad8f5-107">Headers</span></span>](#Headers)  
[<span data-ttu-id="ad8f5-108">Recherche d’un appareil Kinect</span><span class="sxs-lookup"><span data-stu-id="ad8f5-108">Finding a Kinect Device</span></span>](#Finding-a-Kinect-Device)  
[<span data-ttu-id="ad8f5-109">Démarrer les caméras</span><span class="sxs-lookup"><span data-stu-id="ad8f5-109">Starting the Cameras</span></span>](#Starting-the-Cameras)  
[<span data-ttu-id="ad8f5-110">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="ad8f5-110">Error Handling</span></span>](#Error-Handling)  
[<span data-ttu-id="ad8f5-111">Source complet</span><span class="sxs-lookup"><span data-stu-id="ad8f5-111">Full Source</span></span>](#Full-Source)  

<span data-ttu-id="ad8f5-112">**Voici les fonctions que nous allons utiliser :**</span><span class="sxs-lookup"><span data-stu-id="ad8f5-112">**Here are the functions we'll use:**</span></span>  
[`k4a_device_get_installed_count()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-installed-count)  
[`k4a_device_open()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-open)  
[`k4a_device_get_serialnum()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-serialnum)  
[`k4a_device_start_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-cameras)  
[`k4a_device_stop_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-stop-cameras)  
[`k4a_device_close()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-close)

## <a name="headers"></a><span data-ttu-id="ad8f5-113">En-têtes</span><span class="sxs-lookup"><span data-stu-id="ad8f5-113">Headers</span></span>
<span data-ttu-id="ad8f5-114">Il existe un seul en-tête dont vous avez besoin, et qui est k4a.h !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-114">There's only one header that you'll need, and that's k4a.h!</span></span> <span data-ttu-id="ad8f5-115">Assurez-vous que votre compilateur de choix est configurée avec les lib du SDK et inclure les dossiers.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-115">Make sure your compiler of choice is set up with the SDK's lib and include folders.</span></span> <span data-ttu-id="ad8f5-116">Vous devez également les fichiers k4a.lib et k4a.dll liés.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-116">You'll also need the k4a.lib and k4a.dll files linked up.</span></span>
```C
#include <k4a/k4a.h>
```

## <a name="finding-a-kinect-device"></a><span data-ttu-id="ad8f5-117">Recherche d’un appareil Kinect</span><span class="sxs-lookup"><span data-stu-id="ad8f5-117">Finding a Kinect Device</span></span>

![](img/Serial.png)

<span data-ttu-id="ad8f5-118">Plusieurs appareils Azure Kinect DK peuvent être connectés à votre ordinateur !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-118">Multiple Azure Kinect DK devices can be connected to your computer!</span></span> <span data-ttu-id="ad8f5-119">Nous allons tout d’abord commencer par déterminer combien, ou si une est connectée à l’aide du tout la [ `k4a_device_get_installed_count` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-installed-count) (fonction).</span><span class="sxs-lookup"><span data-stu-id="ad8f5-119">We'll first start by finding out how many, or if any are connected at all using the [`k4a_device_get_installed_count`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-installed-count) function.</span></span> <span data-ttu-id="ad8f5-120">Cette fonction doit fonctionner immédiatement, sans aucune installation supplémentaire !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-120">This function should work right away, without any additional setup!</span></span>

```C
uint32_t count = k4a_device_get_installed_count();
```

<span data-ttu-id="ad8f5-121">Une fois que vous avez déterminé Il est en fait un appareil connecté à l’ordinateur, vous pouvez l’ouvrir à l’aide de [ `k4a_device_open` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-open).</span><span class="sxs-lookup"><span data-stu-id="ad8f5-121">Once you've determined there is actually a device connected to the computer, you can open it using [`k4a_device_open`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-open).</span></span> <span data-ttu-id="ad8f5-122">Vous pouvez fournir l’index de l’appareil que vous souhaitez ouvrir, ou vous pouvez simplement utiliser [ `K4A_DEVICE_DEFAULT` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-DEVICE-DEFAULT) pour le premier.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-122">You can provide the index of the device you want to open, or you can just use [`K4A_DEVICE_DEFAULT`](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-DEVICE-DEFAULT) for the first one.</span></span>

```C
// Open the first plugged in Kinect device
k4a_device_t device = NULL;
k4a_device_open(K4A_DEVICE_DEFAULT, &device);
```
<span data-ttu-id="ad8f5-123">Comme avec la plupart des éléments dans l’API k4a, lorsque vous ouvrez un élément, vous devez également le fermer lorsque vous avez terminé avec lui !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-123">As with most things in the k4a API, when you open something, you should also close it when you're finished with it!</span></span> <span data-ttu-id="ad8f5-124">Lorsque vous êtes en cours d’arrêt, n’oubliez pas d’effectuer un appel à [ `k4a_device_close` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-close).</span><span class="sxs-lookup"><span data-stu-id="ad8f5-124">When you're shutting down, remember to make a call to [`k4a_device_close`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-close).</span></span>

```C
k4a_device_close(device);
```

<span data-ttu-id="ad8f5-125">Une fois que l’appareil est ouvert, nous pouvons faire un test simple afin de garantir que tout est OK.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-125">Once the device is open, we can make a really simple test to ensure it's all good.</span></span> <span data-ttu-id="ad8f5-126">Par conséquent, nous allons lire le numéro de série !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-126">So let's read the device's serial number!</span></span>

```C
// Get the size of the serial number
size_t serial_size = 0;
k4a_device_get_serialnum(device, NULL, &serial_size);

// Allocate memory for the serial, then acquire it
char *serial = static_cast<char*>(malloc(serial_size));
k4a_device_get_serialnum(device, serial, &serial_size);
printf("Opened device: %s\n", serial);
free(serial);
```

## <a name="starting-the-cameras"></a><span data-ttu-id="ad8f5-127">Démarrer les caméras</span><span class="sxs-lookup"><span data-stu-id="ad8f5-127">Starting the Cameras</span></span>

<span data-ttu-id="ad8f5-128">Une fois que vous avez ouvert l’appareil, vous devez configurer l’appareil photo avec un [ `k4a_device_configuration_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-configuration-t) objet !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-128">Once you've opened the device, you'll need to configure the camera with a [`k4a_device_configuration_t`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-configuration-t) object!</span></span> <span data-ttu-id="ad8f5-129">Configuration de la caméra a un nombre d’options différentes, et vous devez choisir les paramètres qui correspondent le mieux à votre propre scénario.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-129">Camera configuration has a number of different options, and you'll need to choose the settings that best fit your own scenario.</span></span>

```C
// Configure a stream of 4096x3072 BRGA color data at 15 frames per second
k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
config.camera_fps       = K4A_FRAMES_PER_SECOND_15;
config.color_format     = K4A_IMAGE_FORMAT_COLOR_BGRA32;
config.color_resolution = K4A_COLOR_RESOLUTION_3072P;

// Start the camera with the given configuration
k4a_device_start_cameras(device, &config)

// ...Camera capture and application specific code would go here...

// Shut down the camera when finished with application logic
k4a_device_stop_cameras(device);
```

<span data-ttu-id="ad8f5-130">Pour plus d’informations de configuration sur le __couleur__ appareil photo, [extraire ce document]()!</span><span class="sxs-lookup"><span data-stu-id="ad8f5-130">For configuration details about the __color__ camera, [check out this document]()!</span></span>  
<span data-ttu-id="ad8f5-131">Pour plus d’informations de configuration sur le __profondeur__ appareil photo, [extraire ce document]()!</span><span class="sxs-lookup"><span data-stu-id="ad8f5-131">For configuration details about the __depth__ camera, [check out this document]()!</span></span>

## <a name="error-handling"></a><span data-ttu-id="ad8f5-132">Gestion des erreurs</span><span class="sxs-lookup"><span data-stu-id="ad8f5-132">Error Handling</span></span>

<span data-ttu-id="ad8f5-133">Par souci de concision et de clarté, nous ne plus afficher la gestion des erreurs dans des exemples inline.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-133">For the sake of brevity and clarity, we don't show error handling in some inline examples.</span></span> <span data-ttu-id="ad8f5-134">Toutefois, la gestion des erreurs sont toujours importante !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-134">However, error handling is always important!</span></span> <span data-ttu-id="ad8f5-135">De nombreuses fonctions retourne un type de réussite/échec général [ `k4a_result_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-result-t), ou une variante plus spécifique avec des informations détaillées telles que [ `k4a_wait_result_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-wait-result-t).</span><span class="sxs-lookup"><span data-stu-id="ad8f5-135">Many functions will return a general success/failure type [`k4a_result_t`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-result-t), or a more specific variant with detailed information such as [`k4a_wait_result_t`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-wait-result-t).</span></span> <span data-ttu-id="ad8f5-136">Veillez à consulter la documentation ou intellisense d’une fonction spécifique pour afficher les messages d’erreur vous attendez peut-être à voir à partir de celui-ci !</span><span class="sxs-lookup"><span data-stu-id="ad8f5-136">Be sure to check the docs or intellisense of a specific function to see what error messages you might expect to see from it!</span></span>

<span data-ttu-id="ad8f5-137">Ainsi que les types d’erreurs, il est également le [ `K4A_SUCCEEDED` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-SUCCEEDED) et [ `K4A_FAILED` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-FAILED) macros que vous pouvez utiliser avec eux.</span><span class="sxs-lookup"><span data-stu-id="ad8f5-137">Along with the error types, there's also the [`K4A_SUCCEEDED`](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-SUCCEEDED) and [`K4A_FAILED`](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-FAILED) macros that you can use with them.</span></span> <span data-ttu-id="ad8f5-138">Par conséquent, au lieu d’ouvrir juste un appareil k4a, nous pouvons le protéger comme suit :</span><span class="sxs-lookup"><span data-stu-id="ad8f5-138">So instead of just opening a k4a device, we might guard it like this:</span></span>

```C
// Open the first plugged in Kinect device
k4a_device_t device = NULL;
if ( K4A_FAILED( k4a_device_open(K4A_DEVICE_DEFAULT, &device) ) )
{
    printf("Failed to open k4a device!\n");
    return;
}
```

# <a name="full-source"></a><span data-ttu-id="ad8f5-139">Source complet</span><span class="sxs-lookup"><span data-stu-id="ad8f5-139">Full Source</span></span>

```C
#pragma comment(lib, "k4a.lib")
#include <k4a/k4a.h>

#include <stdio.h>
#include <stdlib.h>

int main()
{
    uint32_t count = k4a_device_get_installed_count();
    if (count == 0)
    {
        printf("No k4a devices attached!\n");
        return 0;
    }

    // Open the first plugged in Kinect device
    k4a_device_t device = NULL;
    if (K4A_FAILED(k4a_device_open(K4A_DEVICE_DEFAULT, &device)))
    {
        printf("Failed to open k4a device!\n");
        return 0;
    }

    // Get the size of the serial number
    size_t serial_size = 0;
    k4a_device_get_serialnum(device, NULL, &serial_size);

    // Allocate memory for the serial, then acquire it
    char* serial = static_cast<char*>(malloc(serial_size));
    k4a_device_get_serialnum(device, serial, &serial_size);
    printf("Opened device: %s\n", serial);
    free(serial);

    // Configure a stream of 4096x3072 BRGA color data at 15 frames per second
    k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
    config.camera_fps = K4A_FRAMES_PER_SECOND_15;
    config.color_format = K4A_IMAGE_FORMAT_COLOR_BGRA32;
    config.color_resolution = K4A_COLOR_RESOLUTION_3072P;

    // Start the camera with the given configuration
    if (K4A_FAILED(k4a_device_start_cameras(device, &config)))
    {
        printf("Failed to start cameras!\n");
        k4a_device_close(device);
        return 0;
    }

    // ...Camera capture and application specific code would go here...

    // Shut down the camera when finished with application logic
    k4a_device_stop_cameras(device);
    k4a_device_close(device);

    return 0;
}
```

## <a name="next-lab---reading-depth-datareaddepthmd"></a><span data-ttu-id="ad8f5-140">Atelier suivant - [lecture des données de profondeur](ReadDepth.md)</span><span class="sxs-lookup"><span data-stu-id="ad8f5-140">Next Lab - [Reading Depth Data](ReadDepth.md)</span></span>
