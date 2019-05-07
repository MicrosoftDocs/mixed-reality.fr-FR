# <a name="setting-up"></a>Configuration de

Mise en route avec l’API de DK Kinect Azure ? Ne cherchez plus ! Ce document vous aidera à en cours d’exécution avec un accès à l’appareil !

Tout d’abord, téléchargez et installez le [Azure Kinect DK API](https://github.com/Microsoft/Azure-Kinect-Sensor-SDK) à partir de Github.

**Contenu**  
[En-têtes](#Headers)  
[Recherche d’un appareil Kinect](#Finding-a-Kinect-Device)  
[Démarrer les caméras](#Starting-the-Cameras)  
[Gestion des erreurs](#Error-Handling)  
[Source complet](#Full-Source)  

**Voici les fonctions que nous allons utiliser :**  
[`k4a_device_get_installed_count()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-installed-count)  
[`k4a_device_open()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-open)  
[`k4a_device_get_serialnum()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-serialnum)  
[`k4a_device_start_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-cameras)  
[`k4a_device_stop_cameras()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-stop-cameras)  
[`k4a_device_close()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-close)

## <a name="headers"></a>En-têtes
Il existe un seul en-tête dont vous avez besoin, et qui est k4a.h ! Assurez-vous que votre compilateur de choix est configurée avec les lib du SDK et inclure les dossiers. Vous devez également les fichiers k4a.lib et k4a.dll liés.
```C
#include <k4a/k4a.h>
```

## <a name="finding-a-kinect-device"></a>Recherche d’un appareil Kinect

![](img/Serial.png)

Plusieurs appareils Azure Kinect DK peuvent être connectés à votre ordinateur ! Nous allons tout d’abord commencer par déterminer combien, ou si une est connectée à l’aide du tout la [ `k4a_device_get_installed_count` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-installed-count) (fonction). Cette fonction doit fonctionner immédiatement, sans aucune installation supplémentaire !

```C
uint32_t count = k4a_device_get_installed_count();
```

Une fois que vous avez déterminé Il est en fait un appareil connecté à l’ordinateur, vous pouvez l’ouvrir à l’aide de [ `k4a_device_open` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-open). Vous pouvez fournir l’index de l’appareil que vous souhaitez ouvrir, ou vous pouvez simplement utiliser [ `K4A_DEVICE_DEFAULT` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-DEVICE-DEFAULT) pour le premier.

```C
// Open the first plugged in Kinect device
k4a_device_t device = NULL;
k4a_device_open(K4A_DEVICE_DEFAULT, &device);
```
Comme avec la plupart des éléments dans l’API k4a, lorsque vous ouvrez un élément, vous devez également le fermer lorsque vous avez terminé avec lui ! Lorsque vous êtes en cours d’arrêt, n’oubliez pas d’effectuer un appel à [ `k4a_device_close` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-close).

```C
k4a_device_close(device);
```

Une fois que l’appareil est ouvert, nous pouvons faire un test simple afin de garantir que tout est OK. Par conséquent, nous allons lire le numéro de série !

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

## <a name="starting-the-cameras"></a>Démarrer les caméras

Une fois que vous avez ouvert l’appareil, vous devez configurer l’appareil photo avec un [ `k4a_device_configuration_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-configuration-t) objet ! Configuration de la caméra a un nombre d’options différentes, et vous devez choisir les paramètres qui correspondent le mieux à votre propre scénario.

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

Pour plus d’informations de configuration sur le __couleur__ appareil photo, [extraire ce document]()!  
Pour plus d’informations de configuration sur le __profondeur__ appareil photo, [extraire ce document]()!

## <a name="error-handling"></a>Gestion des erreurs

Par souci de concision et de clarté, nous ne plus afficher la gestion des erreurs dans des exemples inline. Toutefois, la gestion des erreurs sont toujours importante ! De nombreuses fonctions retourne un type de réussite/échec général [ `k4a_result_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-result-t), ou une variante plus spécifique avec des informations détaillées telles que [ `k4a_wait_result_t` ](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-wait-result-t). Veillez à consulter la documentation ou intellisense d’une fonction spécifique pour afficher les messages d’erreur vous attendez peut-être à voir à partir de celui-ci !

Ainsi que les types d’erreurs, il est également le [ `K4A_SUCCEEDED` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-SUCCEEDED) et [ `K4A_FAILED` ](https://review.docs.microsoft.com/en-us/azurekinect/api/K4A-FAILED) macros que vous pouvez utiliser avec eux. Par conséquent, au lieu d’ouvrir juste un appareil k4a, nous pouvons le protéger comme suit :

```C
// Open the first plugged in Kinect device
k4a_device_t device = NULL;
if ( K4A_FAILED( k4a_device_open(K4A_DEVICE_DEFAULT, &device) ) )
{
    printf("Failed to open k4a device!\n");
    return;
}
```

# <a name="full-source"></a>Source complet

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

## <a name="next-lab---reading-depth-datareaddepthmd"></a>Atelier suivant - [lecture des données de profondeur](ReadDepth.md)
