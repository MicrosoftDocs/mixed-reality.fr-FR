# <a name="reading-rgb-data"></a>Lecture de données RVB

**Contenu**  
[Configuration de l’appareil](#Configuring-the-Device)  
[Obtention d’un cadre de couleur](#Getting-a-Color-Frame)  
[Nettoyage](#Cleaning-Up)  
[Source complet](#Full-Source)  

**Voici les fonctions que nous allons utiliser :**  
[`k4a_device_start_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-cameras)  
[`k4a_capture_get_color_image()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-capture-get-color-image)  
[`k4a_image_get_buffer()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-buffer)  
[`k4a_image_get_width_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-width-pixels)  
[`k4a_image_get_height_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-height-pixels)  
[`k4a_image_release()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-release) 

## <a name="configuring-the-device"></a>Configuration de l’appareil

Après avoir [ouverture d’un appareil k4a](), nous allons devoir configurer les caméras pour récupérer des données de couleur ! Il est beaucoup d’options ici également, donc nous allons passer en revue. Voici un exemple rapide de quoi il ressemble à démarrer une caméra de couleur de base vraiment.

```C
// Configure a stream of 1280x720 BGRA color data at 5 frames per second
k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
config.camera_fps       = K4A_FRAMES_PER_SECOND_5;
config.color_format     = K4A_IMAGE_FORMAT_COLOR_BGRA32;
config.color_resolution = K4A_COLOR_RESOLUTION_720P;

k4a_device_start_cameras(device, &config);
```

Le `color_format` nous permet d’indiquer comment nous voulons nos informations de couleur stockées dans la mémoire tampon d’image ! `K4A_IMAGE_FORMAT_COLOR_BGRA32` serait 32 bits par pixel, stockées en tant que 8 bits pour le bleu, vert, rouge et Alpha. Nous utilisons ce format dans les exemples en raison de son aspect pratique, mais si vous souhaitez être concious d’utilisation de mémoire, les autres formats peut-être choix étendu !

|`color_format`||
|--------------|-----------|
|`K4A_IMAGE_FORMAT_COLOR_MJPG`|Les données de couleur seront dans [format JPEG de mouvement](https://en.wikipedia.org/wiki/Motion_JPEG)|
|`K4A_IMAGE_FORMAT_COLOR_NV12`|[YUV](https://en.wikipedia.org/wiki/YUV) couleur espace 4:2 : format 0, NV12, uniquement disponible à l’adresse résolution 720p.|
|`K4A_IMAGE_FORMAT_COLOR_YUY2`|[YUV](https://en.wikipedia.org/wiki/YUV) couleur espace 4:2:2 format YUY2, uniquement disponible à l’adresse résolution 720p.|
|`K4A_IMAGE_FORMAT_COLOR_BGRA32`|Données de couleurs brutes, 32 bits par pixel, classées en tant que bleu, vert, rouge, Alpha|

Lors de l’écriture votre propre conversion YUV peut être aisée, une bibliothèque rapide et robuste pour la conversion YUV trouverez [libyuv](https://chromium.googlesource.com/libyuv/libyuv/).

Le `color_resolution` a également quelques options !

|`color_resolution`|resolution|aspect|champ de vision| |
|------------------|----------|------|-------------|-|
|`K4A_COLOR_RESOLUTION_720P`  | 1280 x 720  | 16:9 | 90x59
|`K4A_COLOR_RESOLUTION_1080P` | 1920 x 1080 | 16:9 | 90x59
|`K4A_COLOR_RESOLUTION_1440P` | 2560 x 1440 | 16:9 | 90x59
|`K4A_COLOR_RESOLUTION_2160P` | 3840 x 2160 | 16:9 | 90x59
|`K4A_COLOR_RESOLUTION_1536P` | 2048 x 1536 | 4:3  | 90x74.3 
|`K4A_COLOR_RESOLUTION_3072P` | 4096 x 3072 | 4:3  | 90x74.3 | Fréquence d’images max 15.

Et bien sûr, le `camera_fps` également.

|camera_fps||
|--|--|
|`K4A_FRAMES_PER_SECOND_5`
|`K4A_FRAMES_PER_SECOND_15`
|`K4A_FRAMES_PER_SECOND_30`

## <a name="getting-a-color-frame"></a>Obtention d’un cadre de couleur

Obtention de données pour un cadre de couleur et un cadre de la profondeur est un processus très similaire ! Tout d’abord, nous obtenons une capture de l’appareil, puis nous extrayons l’image de couleur à partir de celui-ci, et puis nous extraire les données brutes en dehors de cette image.

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

Les données désormais stockées dans `colorDataBRGA` repose sur le format que nous avons indiqué dans la configuration. Étant donné que nous avons demandé `K4A_IMAGE_FORMAT_COLOR_BGRA32`, nous avons un tableau complet des valeurs de couleur 32 bits stockées dans BGRA order !

Dans ce cas, les fichiers .tga stockent des couleurs dans l’ordre BGR déjà ! Et étant donné que notre fonction enregistrement peut ignorer le canal alpha avec ces arguments, nous pouvons simplement transmettre les données d’image est !

## <a name="cleaning-up"></a>Nettoyage

Et comme toujours, n’oubliez pas de libérer vos ressources quand vous avez terminé avec eux !
```C
// Release all allocated resources, and shut down the Kinect
k4a_image_release(colors);
k4a_capture_release(capture);

k4a_device_stop_cameras(device);
k4a_device_close(device);
```

## <a name="full-source"></a>Source complet

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

## <a name="next-lab---mixing-color-and-depth-datamixdepthandrgbmd"></a>Atelier suivant - [mélange de couleur et profondeur](MixDepthAndRGB.md)