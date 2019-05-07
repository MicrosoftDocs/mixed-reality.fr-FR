# <a name="accessing-the-imu"></a><span data-ttu-id="51f49-101">L’accès à l’IMU</span><span class="sxs-lookup"><span data-stu-id="51f49-101">Accessing the IMU</span></span>

<span data-ttu-id="51f49-102">Azure Kinect DK contient une unité de mesure inertielle (IMU) !</span><span class="sxs-lookup"><span data-stu-id="51f49-102">Azure Kinect DK contains an Inertial Measurement Unit (IMU)!</span></span> <span data-ttu-id="51f49-103">Cela peut être utile pour la détermination de mouvement et l’orientation de l’appareil lors de la capture.</span><span class="sxs-lookup"><span data-stu-id="51f49-103">This can be useful for helping to determine motion and orientation of the device during capture.</span></span> <span data-ttu-id="51f49-104">En particulier si votre appareil n’est pas fixe !</span><span class="sxs-lookup"><span data-stu-id="51f49-104">Especially if you device isn't stationary!</span></span>

<span data-ttu-id="51f49-105">**Contenu :**</span><span class="sxs-lookup"><span data-stu-id="51f49-105">**Contents:**</span></span>  
[<span data-ttu-id="51f49-106">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="51f49-106">Configuration and Setup</span></span>](#Configuration-and-Setup)  
[<span data-ttu-id="51f49-107">Obtention de données</span><span class="sxs-lookup"><span data-stu-id="51f49-107">Getting Data</span></span>](#Getting-Data)  
[<span data-ttu-id="51f49-108">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="51f49-108">Cleaning Up</span></span>](#Cleaning-Up)  
[<span data-ttu-id="51f49-109">Source complet</span><span class="sxs-lookup"><span data-stu-id="51f49-109">Full Source</span></span>](#Full-Source)  

<span data-ttu-id="51f49-110">**Voici les fonctions que nous allons utiliser :**</span><span class="sxs-lookup"><span data-stu-id="51f49-110">**Here are the functions we'll use:**</span></span>  
[`k4a_device_start_imu()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-start-imu)  
[`k4a_device_stop_imu()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-stop-imu)  
[`k4a_device_get_imu_sample()`](https://review.docs.microsoft.com/en-us/azurekinect/api/k4a-device-get-imu-sample)  

## <a name="configuration-and-setup"></a><span data-ttu-id="51f49-111">Installation et configuration</span><span class="sxs-lookup"><span data-stu-id="51f49-111">Configuration and Setup</span></span>

<span data-ttu-id="51f49-112">Configuration ici est assez simple !</span><span class="sxs-lookup"><span data-stu-id="51f49-112">Configuration here is pretty simple!</span></span> <span data-ttu-id="51f49-113">Ne contient aucun élément, vous devez spécifier le dans la configuration d’appareil pour IMU échantillonnage pour fonctionner, mais vous devrez appeler `k4a_device_start_cameras` avant que cela fonctionne !</span><span class="sxs-lookup"><span data-stu-id="51f49-113">There are no items you need to specify the in the device configuration for IMU sampling to work, but you will need to call `k4a_device_start_cameras` before it'll work!</span></span> <span data-ttu-id="51f49-114">Au lieu de cela, vous allez effectuer un appel à `k4a_device_start_imu` après le démarrage de caméras.</span><span class="sxs-lookup"><span data-stu-id="51f49-114">Instead, you'll make a call to `k4a_device_start_imu` after starting the cameras.</span></span>

```C
// Cameras need to be 'started' even if all we want is the IMU
k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
k4a_device_start_cameras(device, &config);

// Start up the IMU sensors
k4a_device_start_imu(device);
```

## <a name="getting-data"></a><span data-ttu-id="51f49-115">Obtention de données</span><span class="sxs-lookup"><span data-stu-id="51f49-115">Getting Data</span></span>

<span data-ttu-id="51f49-116">![Image de l’application exemple IMU](img/IMU.png "Voici ce que nous allons créer un exemple !")</span><span class="sxs-lookup"><span data-stu-id="51f49-116">![IMU sample app image](img/IMU.png "Here's what we'll build as an example!")</span></span>

<span data-ttu-id="51f49-117">L’IMU fournit des données à un taux de 1.6 kHz !</span><span class="sxs-lookup"><span data-stu-id="51f49-117">The IMU provides data at a rate of 1.6kHz!</span></span> <span data-ttu-id="51f49-118">C’est une grande quantité de données, et cela signifie que si vous avez uniquement besoin dessus chaque fois qu’un frame de profondeur/couleur est disponible, vous accumulerez probablement tout à fait une file d’attente d’échantillons IMU vous attend !</span><span class="sxs-lookup"><span data-stu-id="51f49-118">That's a lot of data, and this means that if you're only looking at it each time a depth/color frame is available, you'll likely have quite a queue of IMU samples waiting for you!</span></span> <span data-ttu-id="51f49-119">Notez que ces données ne sont pas une orientation ou position, mais au lieu de cela, une mesure de la force actuellement appliquée à l’appareil.</span><span class="sxs-lookup"><span data-stu-id="51f49-119">Note that this data is not an orientation or position, but rather, a measure of the force currently applied to the device.</span></span>

<span data-ttu-id="51f49-120">Nous pouvons saisir un exemple et le supprime de la file d’attente en appelant `k4a_device_get_imu_sample` avec un délai d’attente de 0 milliseconde.</span><span class="sxs-lookup"><span data-stu-id="51f49-120">We can grab a sample and remove it from the queue by calling `k4a_device_get_imu_sample` with a timeout of 0 milliseconds.</span></span> <span data-ttu-id="51f49-121">Il reviendrai `K4A_WAIT_RESULT_SUCCEEDED` tant qu’il a un exemple disponible !</span><span class="sxs-lookup"><span data-stu-id="51f49-121">It'll return `K4A_WAIT_RESULT_SUCCEEDED` as long as it has a sample available!</span></span>

<span data-ttu-id="51f49-122">Voici un exemple de la somme de tous les exemples actuellement dans la file d’attente et l’impression de la moyenne.</span><span class="sxs-lookup"><span data-stu-id="51f49-122">Here's an example of summing all the samples currently in the queue, and printing the average.</span></span> 

```C
k4a_float3_t gyro_sum  = {0};
k4a_float3_t acc_sum   = {0};
int32_t      sum_count = 0;

// Sum the current queue of IMU samples
k4a_imu_sample_t sample;
while (k4a_device_get_imu_sample(device, &sample, 0) == K4A_WAIT_RESULT_SUCCEEDED)
{
    gyro_sum.xyz = { 
        gyro_sum.xyz.x + sample.gyro_sample.xyz.x, 
        gyro_sum.xyz.y + sample.gyro_sample.xyz.y, 
        gyro_sum.xyz.z + sample.gyro_sample.xyz.z };
    acc_sum.xyz = { 
        acc_sum.xyz.x + sample.acc_sample.xyz.x,  
        acc_sum.xyz.y + sample.acc_sample.xyz.y,  
        acc_sum.xyz.z + sample.acc_sample.xyz.z };
    sum_count += 1;
    samples   += 1;
}

// If we got any samples, print out their average!
if (sum_count > 0)
{
    k4a_float3_t gyro_avg = {
        gyro_sum.xyz.x / sum_count,
        gyro_sum.xyz.y / sum_count,
        gyro_sum.xyz.z / sum_count };
    k4a_float3_t acc_avg = {
        acc_sum.xyz.x / sum_count,
        acc_sum.xyz.y / sum_count,
        acc_sum.xyz.z / sum_count };

    printf("<%6.2f, %6.2f, %6.2f>   ", gyro_avg.xyz.x, gyro_avg.xyz.y, gyro_avg.xyz.z);
    printf("<%6.2f, %6.2f, %6.2f>", acc_avg.xyz.x, acc_avg.xyz.y, acc_avg.xyz.z);

    // Write backspaces so we'll overwrite this line next time
    printf("\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b");
    printf("\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b");
}
```

## <a name="cleaning-up"></a><span data-ttu-id="51f49-123">Nettoyage</span><span class="sxs-lookup"><span data-stu-id="51f49-123">Cleaning Up</span></span>

<span data-ttu-id="51f49-124">Comme toujours, relâchez tout lorsque vous avez terminé  :)</span><span class="sxs-lookup"><span data-stu-id="51f49-124">And as always, release everything when you're finished :)</span></span>

```C
// Release all allocated resources, and shut down the Kinect
k4a_device_stop_imu(device);
k4a_device_stop_cameras(device);
k4a_device_close(device);
```

# <a name="full-source"></a><span data-ttu-id="51f49-125">Source complet</span><span class="sxs-lookup"><span data-stu-id="51f49-125">Full Source</span></span>

```C
#pragma comment(lib, "k4a.lib")
#include <k4a/k4a.h>

#include <stdio.h>
#include <stdlib.h>

void main()
{
    // Open the first plugged in Kinect device
    k4a_device_t device = NULL;
    k4a_device_open(K4A_DEVICE_DEFAULT, &device);

    // Cameras need to be 'started' even if all we want is the IMU
    k4a_device_configuration_t config = K4A_DEVICE_CONFIG_INIT_DISABLE_ALL;
    k4a_device_start_cameras(device, &config);

    // Start up the IMU sensors
    k4a_device_start_imu(device);

    // Display 10,000 samples as fast as they arrive
    printf("Sampling 10,000 times.\n");
    printf("Gyroscope radians/s:       Accelerometer meters/s^2:\n");
    int32_t samples = 0;
    while (samples < 10000)
    {
        k4a_float3_t gyro_sum  = {0};
        k4a_float3_t accel_sum = {0};
        int32_t      sum_count = 0;

        // Sum the current queue of IMU samples
        k4a_imu_sample_t sample;
        while (k4a_device_get_imu_sample(device, &sample, 0) == K4A_WAIT_RESULT_SUCCEEDED)
        {
            gyro_sum.xyz = { 
                gyro_sum.xyz.x + sample.gyro_sample.xyz.x, 
                gyro_sum.xyz.y + sample.gyro_sample.xyz.y, 
                gyro_sum.xyz.z + sample.gyro_sample.xyz.z };
            accel_sum.xyz = { 
                accel_sum.xyz.x + sample.acc_sample.xyz.x,  
                accel_sum.xyz.y + sample.acc_sample.xyz.y,  
                accel_sum.xyz.z + sample.acc_sample.xyz.z };
            sum_count += 1;
            samples   += 1;
        }

        // If we got any samples this loop, print out their average!
        if (sum_count > 0)
        {
            k4a_float3_t gyro_avg = {
                gyro_sum.xyz.x / sum_count,
                gyro_sum.xyz.y / sum_count,
                gyro_sum.xyz.z / sum_count };
            k4a_float3_t accel_avg = {
                accel_sum.xyz.x / sum_count,
                accel_sum.xyz.y / sum_count,
                accel_sum.xyz.z / sum_count };

            printf("<%6.2f, %6.2f, %6.2f>   ", gyro_avg.xyz.x, gyro_avg.xyz.y, gyro_avg.xyz.z);
            printf("<%6.2f, %6.2f, %6.2f>", accel_avg.xyz.x, accel_avg.xyz.y, accel_avg.xyz.z);

            // Write backspaces so we'll overwrite this line next time
            printf("\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b");
            printf("\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b\b");
        }
    }
    printf("\nShutting down.\n");

    // Release all allocated resources, and shut down the Kinect
    k4a_device_stop_imu(device);
    k4a_device_stop_cameras(device);
    k4a_device_close(device);
}
```