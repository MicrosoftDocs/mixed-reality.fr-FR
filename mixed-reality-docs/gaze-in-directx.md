---
title: HEAD et surveillez les regards dans DirectX
description: Guide du développeur pour l’utilisation du pointage de regard principal et les yeux dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 05/09/2019
ms.topic: article
keywords: regards, regards principal, chef de suivi, suivi de le œil, directx, entrée, hologrammes
ms.openlocfilehash: edf20a621178d76bfc97477f9f9b2eca200f1318
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414408"
---
# <a name="head-and-eye-gaze-input-in-directx"></a><span data-ttu-id="06b2f-104">Principaux et surveiller les regards entrée dans DirectX</span><span class="sxs-lookup"><span data-stu-id="06b2f-104">Head and eye gaze input in DirectX</span></span>

<span data-ttu-id="06b2f-105">Dans Windows Mixed Reality, yeux et regards principal entrée est utilisée pour déterminer ce que l’utilisateur consulte.</span><span class="sxs-lookup"><span data-stu-id="06b2f-105">In Windows Mixed Reality, eye and head gaze input is used to determine what the user is looking at.</span></span> <span data-ttu-id="06b2f-106">Cela peut être utilisé pour les modèles d’entrée principaux tels que le lecteur [head regards et validation](gaze-and-commit.md)et également pour fournir un contexte pour les types d’interactions.</span><span class="sxs-lookup"><span data-stu-id="06b2f-106">This can be used to drive primary input models such as [head gaze and commit](gaze-and-commit.md), and also to provide context for types of interactions.</span></span> <span data-ttu-id="06b2f-107">Il existe deux types de regards vecteurs disponibles via l’API : head regards et regards de œil.</span><span class="sxs-lookup"><span data-stu-id="06b2f-107">There are two types of gaze vectors available through the API: head gaze and eye gaze.</span></span>  <span data-ttu-id="06b2f-108">Les deux sont fournis sous forme de trois dimensions ray avec une origine et la direction.</span><span class="sxs-lookup"><span data-stu-id="06b2f-108">Both are provided as a three dimensional ray with an origin and direction.</span></span> <span data-ttu-id="06b2f-109">Les applications peuvent ensuite raycast dans leur arrière-plan ou le monde réel et déterminer ce que l’utilisateur cible.</span><span class="sxs-lookup"><span data-stu-id="06b2f-109">Applications can then raycast into their scenes, or the real world, and determine what the user is targeting.</span></span>

<span data-ttu-id="06b2f-110">**Utilisation de la tête** représente la direction dans laquelle la tête de l’utilisateur est référencée dans.</span><span class="sxs-lookup"><span data-stu-id="06b2f-110">**Head gaze** represents the direction that the user's head is pointed in.</span></span> <span data-ttu-id="06b2f-111">Pensez-y comme à la position et la direction avant de l’appareil lui-même, avec la position qui représente le centre de point entre les deux affichages.</span><span class="sxs-lookup"><span data-stu-id="06b2f-111">Think of this as the position and forward direction of the device itself, with the position representing the center point between the two displays.</span></span>  <span data-ttu-id="06b2f-112">Head regards est disponible sur tous les appareils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="06b2f-112">Head gaze is available on all Mixed Reality devices.</span></span>

<span data-ttu-id="06b2f-113">**Les regards yeux** représente la direction dans laquelle vous cherchent à yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="06b2f-113">**Eye gaze** represents the direction that the user's eyes are looking towards.</span></span> <span data-ttu-id="06b2f-114">L’origine se trouve entre les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="06b2f-114">The origin is located between the user's eyes.</span></span>  <span data-ttu-id="06b2f-115">Il est disponible sur les appareils de réalité mixte qui incluent un système de suivi de le œil.</span><span class="sxs-lookup"><span data-stu-id="06b2f-115">It is available on Mixed Reality devices that include an eye tracking system.</span></span>

<span data-ttu-id="06b2f-116">Head et surveillez les rayons du pointage de regard sont accessibles via le [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API.</span><span class="sxs-lookup"><span data-stu-id="06b2f-116">Both head and eye gaze rays are accessible through the  [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API.</span></span> <span data-ttu-id="06b2f-117">Il vous suffit d’appeler [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose à l’horodatage spécifié et [système de coordonnées](coordinate-systems-in-directx.md).</span><span class="sxs-lookup"><span data-stu-id="06b2f-117">Simply call [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object at the specified timestamp and [coordinate system](coordinate-systems-in-directx.md).</span></span> <span data-ttu-id="06b2f-118">Ce SpatialPointerPose contient un principal du pointage de regard origine et la direction.</span><span class="sxs-lookup"><span data-stu-id="06b2f-118">This SpatialPointerPose contains a head gaze origin and direction.</span></span> <span data-ttu-id="06b2f-119">Il contient également une origine des regards yeux et la direction si le suivi de le œil est disponible.</span><span class="sxs-lookup"><span data-stu-id="06b2f-119">It also contains an eye gaze origin and direction if eye tracking is available.</span></span>

## <a name="using-head-gaze"></a><span data-ttu-id="06b2f-120">À l’aide des regards principal</span><span class="sxs-lookup"><span data-stu-id="06b2f-120">Using head gaze</span></span>

<span data-ttu-id="06b2f-121">Pour accéder à la tête du pointage de regard, démarrez en appelant [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose.</span><span class="sxs-lookup"><span data-stu-id="06b2f-121">To access the head gaze, start by calling  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object.</span></span> <span data-ttu-id="06b2f-122">Vous devez transmettre les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="06b2f-122">You need to pass the following parameters.</span></span>
 - <span data-ttu-id="06b2f-123">Un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) qui représente le système de coordonnées de votre choix pour les regards principal.</span><span class="sxs-lookup"><span data-stu-id="06b2f-123">A [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) that represents the desired coordinate system for the head gaze.</span></span> <span data-ttu-id="06b2f-124">Ceci est représenté par le *coordinateSystem* variable dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="06b2f-124">This is represented by the *coordinateSystem* variable in the following code.</span></span> <span data-ttu-id="06b2f-125">Pour plus d’informations, visitez notre [systèmes de coordonnées](coordinate-systems-in-directx.md) guide du développeur.</span><span class="sxs-lookup"><span data-stu-id="06b2f-125">For more information, visit our [coordinate systems](coordinate-systems-in-directx.md) developer guide.</span></span>
 - <span data-ttu-id="06b2f-126">Un [Timestamp](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) qui représente l’heure exacte de la pose principale demandée.</span><span class="sxs-lookup"><span data-stu-id="06b2f-126">A [Timestamp](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) that represents the exact time of the head pose requested.</span></span>  <span data-ttu-id="06b2f-127">En règle générale, vous allez utiliser un horodatage qui correspond à la fois lorsque le frame actuel s’affiche.</span><span class="sxs-lookup"><span data-stu-id="06b2f-127">Typically you will use a timestamp that corresponds to the time when the current frame will be displayed.</span></span> <span data-ttu-id="06b2f-128">Vous pouvez obtenir cet horodatage affichage prévues à partir d’un [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) objet, qui est accessible via actuel [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).</span><span class="sxs-lookup"><span data-stu-id="06b2f-128">You can get this predicted display timestamp from a  [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) object, which is accessible through the current [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).</span></span>  <span data-ttu-id="06b2f-129">Cet objet HolographicFramePrediction est représenté par le *prédiction* variable dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="06b2f-129">This HolographicFramePrediction object is represented by the *prediction* variable in the following code.</span></span>

 <span data-ttu-id="06b2f-130">Une fois que vous avez un SpatialPointerPose valide, la position de tête et vers l’avant sont accessibles en tant que propriétés.</span><span class="sxs-lookup"><span data-stu-id="06b2f-130">Once you have a valid SpatialPointerPose, the head position and forward direction are accessible as properties.</span></span>  <span data-ttu-id="06b2f-131">Le code suivant montre comment y accéder.</span><span class="sxs-lookup"><span data-stu-id="06b2f-131">The following code  shows how to access them.</span></span>

 ```cpp
using namespace winrt::Windows::UI::Input::Spatial;
using namespace winrt::Windows::Foundation::Numerics;

SpatialPointerPose pointerPose = SpatialPointerPose::TryGetAtTimestamp(coordinateSystem, prediction.Timestamp());
if (pointerPose)
{
    float3 headPosition = pointerPose.Head().Position();
    float3 headForwardDirection = pointerPose.Head().ForwardDirection();

    // Do something with the head gaze
}
```

## <a name="using-eye-gaze"></a><span data-ttu-id="06b2f-132">À l’aide du pointage de regard œil</span><span class="sxs-lookup"><span data-stu-id="06b2f-132">Using eye gaze</span></span>

<span data-ttu-id="06b2f-133">L’API de regards yeux est très similaire à regards principal.</span><span class="sxs-lookup"><span data-stu-id="06b2f-133">The eye gaze API is very similar to head gaze.</span></span>  <span data-ttu-id="06b2f-134">Il utilise le même [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API, qui fournit un rayon origine et la direction que vous pouvez raycast par rapport à votre scène.</span><span class="sxs-lookup"><span data-stu-id="06b2f-134">It uses the same  [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API, which provides a ray origin and direction that you can raycast against your scene.</span></span>  <span data-ttu-id="06b2f-135">La seule différence est que vous devez explicitement activer le suivi des yeux avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="06b2f-135">The only difference is that you need to explicitly enable eye tracking before using it.</span></span> <span data-ttu-id="06b2f-136">Pour ce faire, vous devez effectuer deux étapes :</span><span class="sxs-lookup"><span data-stu-id="06b2f-136">For this, you need to do two steps:</span></span>
1. <span data-ttu-id="06b2f-137">Demander l’autorisation d’utilisateur à utiliser les yeux dans votre application.</span><span class="sxs-lookup"><span data-stu-id="06b2f-137">Request user permission to use eye tracking in your app.</span></span>
2. <span data-ttu-id="06b2f-138">Activer la fonctionnalité « Entrée utilisation » dans votre manifeste du package.</span><span class="sxs-lookup"><span data-stu-id="06b2f-138">Enable the "Gaze Input" capability in your package manifest.</span></span>

### <a name="requesting-access-to-gaze-input"></a><span data-ttu-id="06b2f-139">Demande d’accès à l’utilisation d’entrée</span><span class="sxs-lookup"><span data-stu-id="06b2f-139">Requesting access to gaze input</span></span>
<span data-ttu-id="06b2f-140">Lors du démarrage de votre application, appelez [EyesPose::RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) pour demander l’accès pour le suivi des yeux.</span><span class="sxs-lookup"><span data-stu-id="06b2f-140">When your app is starting up, call [EyesPose::RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) to request access to eye tracking.</span></span> <span data-ttu-id="06b2f-141">Le système demande à l’utilisateur si nécessaire et retourner [GazeInputAccessStatus::Allowed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.gazeinputaccessstatus) une fois que l’accès a été accordé.</span><span class="sxs-lookup"><span data-stu-id="06b2f-141">The system will prompt the user if needed, and return [GazeInputAccessStatus::Allowed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.gazeinputaccessstatus) once access has been granted.</span></span> <span data-ttu-id="06b2f-142">Il s’agit d’un appel asynchrone, elle nécessite un peu de gestion supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="06b2f-142">This is an asynchronous call, so it requires a bit of extra management.</span></span> <span data-ttu-id="06b2f-143">L’exemple suivant démarre un std::thread détachée à attendre le résultat, qui est stockée à une variable de membre appelée *m_isEyeTrackingEnabled*.</span><span class="sxs-lookup"><span data-stu-id="06b2f-143">The following example spins up a detached std::thread to wait for the result, which it stores to a member variable called *m_isEyeTrackingEnabled*.</span></span>

```cpp
using namespace winrt::Windows::Perception::People;
using namespace winrt::Windows::UI::Input;

std::thread requestAccessThread([this]()
{
    auto status = EyesPose::RequestAccessAsync().get();

    if (status == GazeInputAccessStatus::Allowed)
        m_isEyeTrackingEnabled = true;
    else
        m_isEyeTrackingEnabled = false;
});

requestAccessThread.detach();

```
<span data-ttu-id="06b2f-144">À partir d’un thread détaché est qu’une seule option pour la gestion des appels asynchrones.</span><span class="sxs-lookup"><span data-stu-id="06b2f-144">Starting a detached thread is just one option for handling async calls.</span></span>  <span data-ttu-id="06b2f-145">Vous pouvez également utiliser la nouvelle [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) fonctionnalités prises en charge par C++/WinRT.</span><span class="sxs-lookup"><span data-stu-id="06b2f-145">Alternatively, you could use the new [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) functionality supported by C++/WinRT.</span></span>
<span data-ttu-id="06b2f-146">Voici un autre exemple de demande d’autorisation utilisateur :</span><span class="sxs-lookup"><span data-stu-id="06b2f-146">Here is another example for asking for user permission:</span></span>
-   <span data-ttu-id="06b2f-147">EyesPose::IsSupported() permet à l’application déclencher la boîte de dialogue d’autorisation uniquement s’il existe un suivi de l’oeil.</span><span class="sxs-lookup"><span data-stu-id="06b2f-147">EyesPose::IsSupported() allows the application to trigger the permission dialog only if there is an eye tracker.</span></span>
-   <span data-ttu-id="06b2f-148">GazeInputAccessStatus m_gazeInputAccessStatus ; Cela vise à éviter surgit à l’invite d’autorisation indéfiniment.</span><span class="sxs-lookup"><span data-stu-id="06b2f-148">GazeInputAccessStatus m_gazeInputAccessStatus; // This is to prevent popping up the permission prompt over and over again.</span></span>

```cpp
GazeInputAccessStatus m_gazeInputAccessStatus; // This is to prevent popping up the permission prompt over and over again.

// This will trigger to show the permission prompt to the user.
// Ask for access if there is a corresponding device and registry flag did not disable it.
if (Windows::Perception::People::EyesPose::IsSupported() &&
   (m_gazeInputAccessStatus == GazeInputAccessStatus::Unspecified))
{ 
    Concurrency::create_task(Windows::Perception::People::EyesPose::RequestAccessAsync()).then(
    [this](GazeInputAccessStatus status)
    {
        // GazeInputAccessStatus::{Allowed, DeniedBySystem, DeniedByUser, Unspecified}
            m_gazeInputAccessStatus = status;
        
        // Let's be sure to not ask again.
        if(status == GazeInputAccessStatus::Unspecified)
        {
                m_gazeInputAccessStatus = GazeInputAccessStatus::DeniedBySystem;    
        }
    });
}

```


### <a name="declaring-the-gaze-input-capability"></a><span data-ttu-id="06b2f-149">Déclarer la *entrée regards* fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="06b2f-149">Declaring the *Gaze Input* capability</span></span>

<span data-ttu-id="06b2f-150">Double-cliquez sur le fichier appxmanifest dans *l’Explorateur de solutions*.</span><span class="sxs-lookup"><span data-stu-id="06b2f-150">Double click the appxmanifest file in *Solution Explorer*.</span></span>  <span data-ttu-id="06b2f-151">Puis accédez à la *fonctionnalités* section et vérifier le *entrée regards* fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="06b2f-151">Then navigate to the *Capabilities* section and check the *Gaze Input* capability.</span></span> 

![Capacité d’entrée du pointage de regard](images/gaze-input-capability.png)

<span data-ttu-id="06b2f-153">Cette opération ajoute les lignes suivantes à la *Package* section dans le fichier appxmanifest :</span><span class="sxs-lookup"><span data-stu-id="06b2f-153">This adds the following lines to the *Package* section in the appxmanifest file:</span></span>
```xml
  <Capabilities>
    <DeviceCapability Name="gazeInput" />
  </Capabilities>
```

### <a name="getting-the-eye-gaze-ray"></a><span data-ttu-id="06b2f-154">Obtenir le rayon de regards œil</span><span class="sxs-lookup"><span data-stu-id="06b2f-154">Getting the eye gaze ray</span></span>
<span data-ttu-id="06b2f-155">Une fois que vous avez reçu l’accès à ET, vous êtes libre saisir le rayon de regards yeux chaque trame.</span><span class="sxs-lookup"><span data-stu-id="06b2f-155">Once you have received access to ET, you are free to grab the eye gaze ray every frame.</span></span>  <span data-ttu-id="06b2f-156">Comme avec les regards principal, obtenir le [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) en appelant [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec un horodatage souhaité et d’un système de coordonnées.</span><span class="sxs-lookup"><span data-stu-id="06b2f-156">Just as with head gaze, get the [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) by calling [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with a desired timestamp and coordinate system.</span></span> <span data-ttu-id="06b2f-157">Contient le SpatialPointerPose un [EyesPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) via la [yeux](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) propriété.</span><span class="sxs-lookup"><span data-stu-id="06b2f-157">The SpatialPointerPose contains an [EyesPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) object through the [Eyes](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) property.</span></span> <span data-ttu-id="06b2f-158">Cela n’est pas null uniquement si le suivi de le œil est activé.</span><span class="sxs-lookup"><span data-stu-id="06b2f-158">This is non-null only if eye tracking is enabled.</span></span> <span data-ttu-id="06b2f-159">À partir de là, vous pouvez vérifier si l’utilisateur dans l’appareil a un œil d’étalonnage de suivi en appelant [EyesPose::IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span><span class="sxs-lookup"><span data-stu-id="06b2f-159">From there you can check if the user in the device has an eye tracking calibration by calling [EyesPose::IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span></span>  <span data-ttu-id="06b2f-160">Ensuite, utilisez le [les regards](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) propriété à obtenir l’un [SpatialRay](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialray) réceptrice le œil les regards position et la direction.</span><span class="sxs-lookup"><span data-stu-id="06b2f-160">Next, use the [Gaze](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) property to get the a [SpatialRay](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialray) contianing the eye gaze position and direction.</span></span> <span data-ttu-id="06b2f-161">La propriété regards peut parfois être null, veillez à vérifier cela.</span><span class="sxs-lookup"><span data-stu-id="06b2f-161">The Gaze property can sometimes be null, so be sure to check for this.</span></span> <span data-ttu-id="06b2f-162">Cela peut est se produire si un utilisateur étalonné ferme temporairement leurs yeux.</span><span class="sxs-lookup"><span data-stu-id="06b2f-162">This can happen is if a calibrated user temporarily closes their eyes.</span></span>

<span data-ttu-id="06b2f-163">Le code suivant montre comment accéder au rayon de regards yeux.</span><span class="sxs-lookup"><span data-stu-id="06b2f-163">The following code shows how to access the eye gaze ray.</span></span>

```cpp
using namespace winrt::Windows::UI::Input::Spatial;
using namespace winrt::Windows::Foundation::Numerics;

SpatialPointerPose pointerPose = SpatialPointerPose::TryGetAtTimestamp(coordinateSystem, prediction.Timestamp());
if (pointerPose)
{
    if (pointerPose.Eyes() && pointerPose.Eyes().IsCalibrationValid())
    {
        if (pointerPose.Eyes().Gaze())
        {
            auto spatialRay = pointerPose.Eyes().Gaze().Value();
            float3 eyeGazeOrigin = spatialRay.Origin;
            float3 eyeGazeDirection = spatialRay.Direction;
            
            // Do something with the eye gaze
        }
    }
}

```

## <a name="correlating-gaze-with-other-inputs"></a><span data-ttu-id="06b2f-164">Corrélation des regards avec les autres entrées</span><span class="sxs-lookup"><span data-stu-id="06b2f-164">Correlating gaze with other inputs</span></span>

<span data-ttu-id="06b2f-165">Parfois, vous constaterez que vous avez besoin une [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) qui correspond à un événement dans le passé.</span><span class="sxs-lookup"><span data-stu-id="06b2f-165">Sometimes you may find that you need a [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) that corresponds with an event in the past.</span></span> <span data-ttu-id="06b2f-166">Par exemple, si l’utilisateur effectue un Air appuyez sur, votre application souhaiterez peut-être savoir qu’ils ont été consultant.</span><span class="sxs-lookup"><span data-stu-id="06b2f-166">For example, if the user performs an Air Tap, your app might want to know what they were looking at.</span></span> <span data-ttu-id="06b2f-167">Pour cela, il vous suffit à l’aide de [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) la trame prédite temps seraient inexacte en raison de la latence entre le traitement du système d’entrée et d’affichage de l’heure.</span><span class="sxs-lookup"><span data-stu-id="06b2f-167">For this purpose, simply using [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with the predicted frame time would be inaccurate because of the latency between system input processing and display time.</span></span> <span data-ttu-id="06b2f-168">En outre, si vous utilisez des regards d’oeil pour le ciblage, nos yeux ont tendance à déplacer même avant la fin d’une action de validation.</span><span class="sxs-lookup"><span data-stu-id="06b2f-168">In addition, if using eye gaze for targeting, our eyes tend to move on even before finishing a commit action.</span></span> <span data-ttu-id="06b2f-169">Cela est moins de problèmes pour un Tap Air simple, mais devient plus importante lors de la combinaison la durée pendant laquelle les commandes vocales avec des mouvements d’oeil rapide.</span><span class="sxs-lookup"><span data-stu-id="06b2f-169">This is less of an issue for a simple Air Tap, but becomes more critical when combining long voice commands with fast eye movements.</span></span> <span data-ttu-id="06b2f-170">Une pour gérer ce scénario consiste à effectuer un appel supplémentaire à [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), à l’aide d’une date et heure historiques qui correspond à l’événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="06b2f-170">One way to handle this scenario is to make an additional call to  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), using a historical timestamp that corresponds to the input event.</span></span>  

<span data-ttu-id="06b2f-171">Toutefois, pour l’entrée qui traverse le SpatialInteractionManager, il existe une méthode plus facile.</span><span class="sxs-lookup"><span data-stu-id="06b2f-171">However, for input that routes through the SpatialInteractionManager, there's an easier method.</span></span> <span data-ttu-id="06b2f-172">Le [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) a son propre [TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) (fonction).</span><span class="sxs-lookup"><span data-stu-id="06b2f-172">The [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) has its very own [TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) function.</span></span> <span data-ttu-id="06b2f-173">Appel qui fournira un parfaitement corrélés [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) sans devinette.</span><span class="sxs-lookup"><span data-stu-id="06b2f-173">Calling that will provide a perfectly correlated [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) without the guesswork.</span></span> <span data-ttu-id="06b2f-174">Pour plus d’informations sur l’utilisation des SpatialInteractionSourceStates, examinons le [mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md) documentation.</span><span class="sxs-lookup"><span data-stu-id="06b2f-174">For more information on working with SpatialInteractionSourceStates, take a look at the [Hands and Motion Controllers in DirectX](hands-and-motion-controllers-in-directx.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="06b2f-175">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="06b2f-175">See also</span></span>
* [<span data-ttu-id="06b2f-176">Modèle d’entrée principal du pointage de regard et validation</span><span class="sxs-lookup"><span data-stu-id="06b2f-176">Head gaze and commit input model</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="06b2f-177">OCULAIRE sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="06b2f-177">Eye-gaze on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="06b2f-178">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="06b2f-178">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
* [<span data-ttu-id="06b2f-179">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="06b2f-179">Voice Input in DirectX</span></span>](voice-input-in-directx.md)
* [<span data-ttu-id="06b2f-180">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="06b2f-180">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
