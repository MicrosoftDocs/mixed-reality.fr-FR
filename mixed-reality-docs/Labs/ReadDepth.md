# <a name="reading-depth-data"></a>Lecture des données de profondeur

Vous avez besoin pour lire les données de profondeur de l’appareil ? Il est facile !

**Contenu**  
[Configuration de l’appareil](#Configuring-the-Device)  
[Profondeur d’accéder aux données](#Acessing-Depth-Data)  
[Nettoyage](#Cleaning-Up)  
[Source complet](#Full-Source)  

**Voici les fonctions que nous allons utiliser :**  
[`k4a_device_start_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-cameras)  
[`k4a_capture_get_depth_image()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-capture-get-depth-image)  
[`k4a_image_get_buffer()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-buffer)  
[`k4a_image_get_width_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-width-pixels)  
[`k4a_image_get_height_pixels()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-get-height-pixels)  
[`k4a_image_release()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-image-release)  

## <a name="configuring-the-device"></a>Configuration de l’appareil

Après avoir [ouverture d’une interface]() à l’appareil Azure Kinect DK, vous devez configurer l’appareil photo pour capturer des données de profondeur. Il existe un seul élément, vous devez vraiment connaître lors de la configuration de profondeur, et c’est le `depth_mode`!

```C
k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
config.depth_mode = K4A_DEPTH_MODE_NFOV_UNBINNED;

k4a_device_start_cameras(device, &config);
```

Ici le `depth_mode` propose quelques choix ! Selon le contexte de notre application, nous pouvons demander nos données de profondeur dans différents formats.

Exécutent des algorithmes de durée limitée sur les données de profondeur ? Sélectionner, par exemple un mode 2X2BINNED il y a moins de données à utiliser ! Vous vous souciez plus ce qui est loin out directement anticipée, au lieu de ce qui est proche et dans la périphérie ? Utiliser un champ de vision étroite avec les modes NFOV !
| [`depth_mode`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-depth-mode-t) | description |
|------------|-------------|
|`K4A_DEPTH_MODE_WFOV_UNBINNED`|Angle de vue large (120 x 120), profondeur (0.25-2.21 m), résolution élevée des données (1 024 x 1 024). A une fréquence d’images maximale de 15.|
|`K4A_DEPTH_MODE_WFOV_2X2BINNED`|Angle de vue large (120 x 120), profondeur (0.25-2,88 m), basse résolution (512 x 512).|
|`K4A_DEPTH_MODE_NFOV_UNBINNED`|Rayures étroites angle de vue (75 x 65), profondeur lointain (0,5-3.86 m), haute résolution (640 x 576).|
|`K4A_DEPTH_MODE_NFOV_2X2BINNED`|Strictes vue (75 x 65), profondeur lointain (0,5-5.46 m), données basse résolution (320 x 288).|
|`K4A_DEPTH_MODE_PASSIVE_IR`|RAW flux à partir de l’appareil photo de runtime d’intégration (1024 x 1024)|
||Profondeur est fournie en dehors de la plage spécifiée en fonction de la réflectivité de l’objet.|

## <a name="acessing-depth-data"></a>Profondeur d’accéder aux données

![](img/Depth.png)

Lorsque nous capturez une image à partir de l’appareil, nous pouvons utiliser `k4a_capture_get_depth_image` et `k4a_image_get_buffer` pour obtenir les données brutes de profondeur !

```C
// Capture a frame
k4a_capture_t capture;
k4a_device_get_capture(device, &capture, K4A_WAIT_INFINITE);

// Get the depth data and information from the current capture
k4a_image_t depth_image  = k4a_capture_get_depth_image(capture);
uint16_t   *depth_buffer = reinterpret_cast<uint16_t*>(k4a_image_get_buffer(depth_image));
int32_t width  = k4a_image_get_width_pixels (depth_image);
int32_t height = k4a_image_get_height_pixels(depth_image);
```

Informations sur la profondeur sont fournies en tant que tableau d’entiers non signés 16 bits, représentant millimètres à partir de l’appareil photo. Le tableau contiendra un zéro si la valeur de profondeur n’est pas présente pour un pixel spécifique.

Dans cet exemple, nous allons simplement convertir les données de profondeur dans une image en nuances de gris et enregistrez-le dans le fichier !

```C
// Write this depth capture to an image file

// Allocate memory for an 8-bit grayscale image
uint8_t *file_color = static_cast<uint8_t *>(malloc(sizeof(uint8_t) * width*height));

// Convert each depth value to a shade of gray!
for (int32_t i = 0; i < width*height; i++)
{
    // Make a gray from the depth, white up close, black at 3 meters in the distance
    float depth_gray = 1-(depth_buffer[i] / 3000.0f);
    // Cap at 1.0, any higher and our uint8_t will overflow and wrap around
    depth_gray = depth_gray > 1.0f ? 1.0f : depth_gray;

    file_color[i] = static_cast<uint8_t>(depth_gray * 255);
}
tga_write("outDepth.tga", width, height, file_color, 1, 3);
free(file_color);
```

## <a name="cleaning-up"></a>Nettoyage

N’oubliez pas d’arrêter et libérer tous les éléments que vous avez alloué ou saisi ! N’oubliez pas que les captures de frame doivent être libérées une fois que vous avez terminé avec eux et avant d’en saisissant un autre frame.

```C
// Release all allocated resources, and shut down the Kinect
k4a_image_release(depth_image);
k4a_capture_release(capture);

k4a_device_stop_cameras(device);
k4a_device_close(device);
```

# <a name="full-source"></a>Source complet

```C
#pragma comment(lib, "k4a.lib")
#include <k4a/k4a.h>

#include <stdio.h>
#include <stdlib.h>

void tga_write(const char *filename, uint32_t width, uint32_t height, uint8_t *data_bgra, uint8_t data_channels, uint8_t file_channels);

int main()
{
    // Open the first plugged in Kinect device
    k4a_device_t device = NULL;
    k4a_device_open(K4A_DEVICE_DEFAULT, &device);

    // Configure the Kinect to open a stream of 1024x1024 wide FOV at 5 frames per second
    k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
    config.camera_fps = K4A_FRAMES_PER_SECOND_5;
    config.depth_mode = K4A_DEPTH_MODE_WFOV_UNBINNED;

    k4a_device_start_cameras(device, &config);

    // Wait until the first capture is available to us
    k4a_capture_t capture;
    k4a_device_get_capture(device, &capture, K4A_WAIT_INFINITE);

    // Get the depth data and information from the current capture
    k4a_image_t depth_image  = k4a_capture_get_depth_image(capture);
    uint16_t   *depth_buffer = reinterpret_cast<uint16_t*>(k4a_image_get_buffer(depth_image));
    int32_t width  = k4a_image_get_width_pixels (depth_image);
    int32_t height = k4a_image_get_height_pixels(depth_image);
    printf("Captured depth image, %dx%d\n", width, height);

    // Write this depth capture to an image file

    // Allocate memory for an 8-bit grayscale image
    uint8_t *file_color = static_cast<uint8_t *>(malloc(sizeof(uint8_t) * width*height));

    // Convert each depth value to a shade of gray!
    for (int32_t i = 0; i < width*height; i++)
    {
        // Make a gray from the depth, white up close, black at 3 meters in the distance
        float depth_gray = 1-(depth_buffer[i] / 3000.0f);
        // Cap at 1.0, any higher and our uint8_t will overflow and wrap around
        depth_gray = depth_gray > 1.0f ? 1.0f : depth_gray;

        file_color[i] = static_cast<uint8_t>(depth_gray * 255);
    }
    tga_write("outDepth.tga", width, height, file_color, 1, 3);
    free(file_color);

    // Release all allocated resources, and shut down the Kinect
    k4a_image_release(depth_image);
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

## <a name="next-lab---reading-rgb-datareadcolormd"></a>Atelier suivant - [lecture des données de RVB](ReadColor.md)