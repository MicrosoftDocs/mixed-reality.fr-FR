# <a name="reading-rgb-data"></a><span data-ttu-id="e597d-101">Lecture de données RVB</span><span class="sxs-lookup"><span data-stu-id="e597d-101">Reading RGB Data</span></span>

<span data-ttu-id="e597d-102">**Contenu**</span><span class="sxs-lookup"><span data-stu-id="e597d-102">**Contents**</span></span>  
[<span data-ttu-id="e597d-103">Configuration de l’appareil</span><span class="sxs-lookup"><span data-stu-id="e597d-103">Configuring the Device</span></span>](#Configuring-the-Device)  
[<span data-ttu-id="e597d-104">Obtention d’un cadre de couleur</span><span class="sxs-lookup"><span data-stu-id="e597d-104">Getting a Color Frame</span></span>](#Getting-a-Color-Frame)  
[<span data-ttu-id="e597d-105">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="e597d-105">Cleaning Up</span></span>](#Cleaning-Up)  
[<span data-ttu-id="e597d-106">Source complet</span><span class="sxs-lookup"><span data-stu-id="e597d-106">Full Source</span></span>](#Full-Source)  

<span data-ttu-id="e597d-107">**Voici les fonctions que nous allons utiliser :**</span><span class="sxs-lookup"><span data-stu-id="e597d-107">**Here are the functions we'll use:**</span></span>  
[`k4a_device_start_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-cameras)  
[`k4a_capture_get_color_image()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-capture-get-color-image)  
[`k4a_image_get_buffer()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-buffer)  
[`k4a_image_get_width_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-width-pixels)  
[`k4a_image_get_height_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-height-pixels)  
[`k4a_image_release()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-release) 

## <a name="configuring-the-device"></a><span data-ttu-id="e597d-108">Configuration de l’appareil</span><span class="sxs-lookup"><span data-stu-id="e597d-108">Configuring the Device</span></span>

<span data-ttu-id="e597d-109">Après avoir [ouverture d’un appareil k4a](), nous allons devoir configurer les caméras pour récupérer des données de couleur !</span><span class="sxs-lookup"><span data-stu-id="e597d-109">After [opening a k4a device](), we'll need to set up the cameras to grab color data!</span></span> <span data-ttu-id="e597d-110">Il est beaucoup d’options ici également, donc nous allons passer en revue.</span><span class="sxs-lookup"><span data-stu-id="e597d-110">There's a lot of options here as well, so we'll go through them.</span></span> <span data-ttu-id="e597d-111">Voici un exemple rapide de quoi il ressemble à démarrer une caméra de couleur de base vraiment.</span><span class="sxs-lookup"><span data-stu-id="e597d-111">Here's a quick example of what it looks like to start up a really basic color camera.</span></span>

```C
// Configure a stream of 1280x720 BGRA color data at 5 frames per second
k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
config.camera_fps       = K4A_FRAMES_PER_SECOND_5;
config.color_format     = K4A_IMAGE_FORMAT_COLOR_BGRA32;
config.color_resolution = K4A_COLOR_RESOLUTION_720P;

k4a_device_start_cameras(device, &config);
```

<span data-ttu-id="e597d-112">Le `color_format` nous permet d’indiquer comment nous voulons nos informations de couleur stockées dans la mémoire tampon d’image !</span><span class="sxs-lookup"><span data-stu-id="e597d-112">The `color_format` allows us to say how we want our color information stored in the image buffer!</span></span> <span data-ttu-id="e597d-113">`K4A_IMAGE_FORMAT_COLOR_BGRA32` serait 32 bits par pixel, stockées en tant que 8 bits pour le bleu, vert, rouge et Alpha.</span><span class="sxs-lookup"><span data-stu-id="e597d-113">`K4A_IMAGE_FORMAT_COLOR_BGRA32` would be 32 bits per pixel, stored as 8 bits each for Blue, Green, Red, and Alpha.</span></span> <span data-ttu-id="e597d-114">Nous utilisons ce format dans les exemples en raison de son aspect pratique, mais si vous souhaitez être concious d’utilisation de mémoire, les autres formats peut-être choix étendu !</span><span class="sxs-lookup"><span data-stu-id="e597d-114">We use this format in the examples due to its convenience, but if you want to be concious of memory usage, other formats may be superior choices!</span></span>

|`color_format`||
|--------------|-----------|
|`K4A_IMAGE_FORMAT_COLOR_MJPG`|<span data-ttu-id="e597d-115">Les données de couleur seront dans [format JPEG de mouvement](https://en.wikipedia.org/wiki/Motion_JPEG)</span><span class="sxs-lookup"><span data-stu-id="e597d-115">Color data will be in [Motion JPEG format](https://en.wikipedia.org/wiki/Motion_JPEG)</span></span>|
|`K4A_IMAGE_FORMAT_COLOR_NV12`|<span data-ttu-id="e597d-116">[YUV](https://en.wikipedia.org/wiki/YUV) couleur espace 4:2 : format 0, NV12, uniquement disponible à l’adresse résolution 720p.</span><span class="sxs-lookup"><span data-stu-id="e597d-116">[YUV](https://en.wikipedia.org/wiki/YUV) color space 4:2:0 format, NV12, only available at 720p resolution.</span></span>|
|`K4A_IMAGE_FORMAT_COLOR_YUY2`|<span data-ttu-id="e597d-117">[YUV](https://en.wikipedia.org/wiki/YUV) couleur espace 4:2:2 format YUY2, uniquement disponible à l’adresse résolution 720p.</span><span class="sxs-lookup"><span data-stu-id="e597d-117">[YUV](https://en.wikipedia.org/wiki/YUV) color space 4:2:2 format, YUY2, only available at 720p resolution.</span></span>|
|`K4A_IMAGE_FORMAT_COLOR_BGRA32`|<span data-ttu-id="e597d-118">Données de couleurs brutes, 32 bits par pixel, classées en tant que bleu, vert, rouge, Alpha</span><span class="sxs-lookup"><span data-stu-id="e597d-118">Raw color data, 32 bits per pixel, ordered as Blue, Green, Red, Alpha</span></span>|

<span data-ttu-id="e597d-119">Lors de l’écriture votre propre conversion YUV peut être aisée, une bibliothèque rapide et robuste pour la conversion YUV trouverez [libyuv](https://chromium.googlesource.com/libyuv/libyuv/).</span><span class="sxs-lookup"><span data-stu-id="e597d-119">While writing your own YUV conversion may be easy enough, a fast, robust library for YUV conversion can be found at [libyuv](https://chromium.googlesource.com/libyuv/libyuv/).</span></span>

<span data-ttu-id="e597d-120">Le `color_resolution` a également quelques options !</span><span class="sxs-lookup"><span data-stu-id="e597d-120">The `color_resolution` also has a couple of options!</span></span>

|`color_resolution`|<span data-ttu-id="e597d-121">resolution</span><span class="sxs-lookup"><span data-stu-id="e597d-121">resolution</span></span>|<span data-ttu-id="e597d-122">aspect</span><span class="sxs-lookup"><span data-stu-id="e597d-122">aspect</span></span>|<span data-ttu-id="e597d-123">champ de vision</span><span class="sxs-lookup"><span data-stu-id="e597d-123">field of view</span></span>| |
|------------------|----------|------|-------------|-|
|`K4A_COLOR_RESOLUTION_720P`  | <span data-ttu-id="e597d-124">1280 x 720</span><span class="sxs-lookup"><span data-stu-id="e597d-124">1280 x 720</span></span>  | <span data-ttu-id="e597d-125">16:9</span><span class="sxs-lookup"><span data-stu-id="e597d-125">16:9</span></span> | <span data-ttu-id="e597d-126">90x59</span><span class="sxs-lookup"><span data-stu-id="e597d-126">90x59</span></span>
|`K4A_COLOR_RESOLUTION_1080P` | <span data-ttu-id="e597d-127">1920 x 1080</span><span class="sxs-lookup"><span data-stu-id="e597d-127">1920 x 1080</span></span> | <span data-ttu-id="e597d-128">16:9</span><span class="sxs-lookup"><span data-stu-id="e597d-128">16:9</span></span> | <span data-ttu-id="e597d-129">90x59</span><span class="sxs-lookup"><span data-stu-id="e597d-129">90x59</span></span>
|`K4A_COLOR_RESOLUTION_1440P` | <span data-ttu-id="e597d-130">2560 x 1440</span><span class="sxs-lookup"><span data-stu-id="e597d-130">2560 x 1440</span></span> | <span data-ttu-id="e597d-131">16:9</span><span class="sxs-lookup"><span data-stu-id="e597d-131">16:9</span></span> | <span data-ttu-id="e597d-132">90x59</span><span class="sxs-lookup"><span data-stu-id="e597d-132">90x59</span></span>
|`K4A_COLOR_RESOLUTION_2160P` | <span data-ttu-id="e597d-133">3840 x 2160</span><span class="sxs-lookup"><span data-stu-id="e597d-133">3840 x 2160</span></span> | <span data-ttu-id="e597d-134">16:9</span><span class="sxs-lookup"><span data-stu-id="e597d-134">16:9</span></span> | <span data-ttu-id="e597d-135">90x59</span><span class="sxs-lookup"><span data-stu-id="e597d-135">90x59</span></span>
|`K4A_COLOR_RESOLUTION_1536P` | <span data-ttu-id="e597d-136">2048 x 1536</span><span class="sxs-lookup"><span data-stu-id="e597d-136">2048 x 1536</span></span> | <span data-ttu-id="e597d-137">4:3</span><span class="sxs-lookup"><span data-stu-id="e597d-137">4:3</span></span>  | <span data-ttu-id="e597d-138">90x74.3</span><span class="sxs-lookup"><span data-stu-id="e597d-138">90x74.3</span></span> 
|`K4A_COLOR_RESOLUTION_3072P` | <span data-ttu-id="e597d-139">4096 x 3072</span><span class="sxs-lookup"><span data-stu-id="e597d-139">4096 x 3072</span></span> | <span data-ttu-id="e597d-140">4:3</span><span class="sxs-lookup"><span data-stu-id="e597d-140">4:3</span></span>  | <span data-ttu-id="e597d-141">90x74.3</span><span class="sxs-lookup"><span data-stu-id="e597d-141">90x74.3</span></span> | <span data-ttu-id="e597d-142">Fréquence d’images max 15.</span><span class="sxs-lookup"><span data-stu-id="e597d-142">Max framerate 15.</span></span>

<span data-ttu-id="e597d-143">Et bien sûr, le `camera_fps` également.</span><span class="sxs-lookup"><span data-stu-id="e597d-143">And of course, the `camera_fps` as well.</span></span>

|<span data-ttu-id="e597d-144">camera_fps</span><span class="sxs-lookup"><span data-stu-id="e597d-144">camera_fps</span></span>||
|--|--|
|`K4A_FRAMES_PER_SECOND_5`
|`K4A_FRAMES_PER_SECOND_15`
|`K4A_FRAMES_PER_SECOND_30`

## <a name="getting-a-color-frame"></a><span data-ttu-id="e597d-145">Obtention d’un cadre de couleur</span><span class="sxs-lookup"><span data-stu-id="e597d-145">Getting a Color Frame</span></span>

<span data-ttu-id="e597d-146">Obtention de données pour un cadre de couleur et un cadre de la profondeur est un processus très similaire !</span><span class="sxs-lookup"><span data-stu-id="e597d-146">Getting data for a color frame and a depth frame is a very similar process!</span></span> <span data-ttu-id="e597d-147">Tout d’abord, nous obtenons une capture de l’appareil, puis nous extrayons l’image de couleur à partir de celui-ci, et puis nous extraire les données brutes en dehors de cette image.</span><span class="sxs-lookup"><span data-stu-id="e597d-147">First we get a capture from the device, then we extract the color image from it, and then we pull the raw data out of that image.</span></span>

```C
// Wait until the first capture is available to us
k4a_capture_t capture;
k4a_device_get_capture(device, &capture, K4A_WAIT_INFINITE);

// Get the color data and information from the current capture
k4a_image_t colors      = k4a_capture_get_color_image(capture);
uint8_t    *colors_bgra = k4a_image_get_buffer(colors);
int width  = k4a_image_get_width_pixels (colors);
int height = k4a_image_get_height_pixels(colors);

// Write this capture to file
tga_write("out.tga", width, height, colorDataBGRA, 4, 3);
```

<span data-ttu-id="e597d-148">Les données désormais stockées dans `colorDataBRGA` repose sur le format que nous avons indiqué dans la configuration.</span><span class="sxs-lookup"><span data-stu-id="e597d-148">The data now stored in `colorDataBRGA` is dependant on the format we indicated in configuration.</span></span> <span data-ttu-id="e597d-149">Étant donné que nous avons demandé `K4A_IMAGE_FORMAT_COLOR_BGRA32`, nous avons un tableau complet des valeurs de couleur 32 bits stockées dans BGRA order !</span><span class="sxs-lookup"><span data-stu-id="e597d-149">Since we asked for `K4A_IMAGE_FORMAT_COLOR_BGRA32`, we have an array full of 32 bit color values stored in BGRA order!</span></span>

<span data-ttu-id="e597d-150">Dans ce cas, les fichiers .tga stockent des couleurs dans l’ordre BGR déjà !</span><span class="sxs-lookup"><span data-stu-id="e597d-150">In this case, .tga files store colors in BGR order already!</span></span> <span data-ttu-id="e597d-151">Et étant donné que notre fonction enregistrement peut ignorer le canal alpha avec ces arguments, nous pouvons simplement transmettre les données d’image est !</span><span class="sxs-lookup"><span data-stu-id="e597d-151">And since our saving function can skip the alpha channel with these arguments, we can just pass the image data as is!</span></span>

## <a name="cleaning-up"></a><span data-ttu-id="e597d-152">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="e597d-152">Cleaning Up</span></span>

<span data-ttu-id="e597d-153">Et comme toujours, n’oubliez pas de libérer vos ressources quand vous avez terminé avec eux !</span><span class="sxs-lookup"><span data-stu-id="e597d-153">And as always, remember to release your resources when you're done with them!</span></span>
```C
// Release all allocated resources, and shut down the Kinect
k4a_image_release(colors);
k4a_capture_release(capture);

k4a_device_stop_cameras(device);
k4a_device_close(device);
```

## <a name="full-source"></a><span data-ttu-id="e597d-154">Source complet</span><span class="sxs-lookup"><span data-stu-id="e597d-154">Full Source</span></span>

```C
#pragma comment(lib, "k4a.lib")
#include <k4a/k4a.h>

#include <stdio.h>
#include <stdlib.h>

void tga_write(const char *filename, uint32_t width, uint32_t height, uint8_t *data_bgra, uint8_t data_channels, uint8_t file_channels);

int main() {
    // Open the first plugged in Kinect device
    k4a_device_t device = NULL;
    k4a_device_open(K4A_DEVICE_DEFAULT, &device);

    // Configure a stream of 1280x720 BRGA data at 5 frames per second
    k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
    config.camera_fps       = K4A_FRAMES_PER_SECOND_5;
    config.color_format     = K4A_IMAGE_FORMAT_COLOR_BGRA32;
    config.color_resolution = K4A_COLOR_RESOLUTION_720P;

    k4a_device_start_cameras(device, &config);

    // Wait until the first capture is available to us
    k4a_capture_t capture;
    k4a_device_get_capture(device, &capture, K4A_WAIT_INFINITE);

    // Get the color data and information from the current capture
    k4a_image_t colors      = k4a_capture_get_color_image(capture);
    uint8_t    *colors_bgra = k4a_image_get_buffer(colors);
    int width  = k4a_image_get_width_pixels (colors);
    int height = k4a_image_get_height_pixels(colors);
    printf("Captured RGB image, %dx%d\n", width, height);

    // Write this capture to file
    tga_write("out.tga", width, height, colors_bgra, 4, 3);

    // Release all allocated resources, and shut down the Kinect
    k4a_image_release(colors);
    k4a_capture_release(capture);

    k4a_device_stop_cameras(device);
    k4a_device_close(device);

    return 0;
}

void tga_write(const char *filename, uint32_t width, uint32_t height, uint8_t *data_bgra, uint8_t data_channels, uint8_t file_channels)
{
    FILE *fp = NULL;
    fopen_s(&fp, filename, "wb");
    if (fp == NULL) return;

    uint8_t header[18] = { 0,0,2,0,0,0,0,0,0,0,0,0, width % 256, (uint8_t)(width / 256), height % 256, (uint8_t)(height / 256), file_channels * 8u, 0x20 };
    fwrite(&header, 18, 1, fp);
    for (uint32_t i = 0; i < width*height; i++)
        for (uint32_t b = 0; b < file_channels; b++)
            fputc(data_bgra[(i*data_channels) + (b%data_channels)], fp);
    fclose(fp);
}
```

## <a name="next-lab---mixing-color-and-depth-datamixdepthandrgbmd"></a><span data-ttu-id="e597d-155">Atelier suivant - [mélange de couleur et profondeur](MixDepthAndRGB.md)</span><span class="sxs-lookup"><span data-stu-id="e597d-155">Next Lab - [Mixing Color and Depth Data](MixDepthAndRGB.md)</span></span>