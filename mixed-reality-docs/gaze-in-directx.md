---
title: Tête et regard de DirectX
description: Guide du développeur pour utiliser le suivi des regards et des yeux en tête dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 05/09/2019
ms.topic: article
keywords: point d’interposition, pointage en tête, suivi des yeux, suivi des yeux, DirectX, entrée, hologrammes
ms.openlocfilehash: edf20a621178d76bfc97477f9f9b2eca200f1318
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414408"
---
# <a name="head-and-eye-gaze-input-in-directx"></a><span data-ttu-id="ba458-104">Entrée en regard de l’en-tête et de l’œil dans DirectX</span><span class="sxs-lookup"><span data-stu-id="ba458-104">Head and eye gaze input in DirectX</span></span>

<span data-ttu-id="ba458-105">Dans Windows Mixed Reality, l’entrée en regard de l’œil et de la tête est utilisée pour déterminer ce que l’utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="ba458-105">In Windows Mixed Reality, eye and head gaze input is used to determine what the user is looking at.</span></span> <span data-ttu-id="ba458-106">Cela peut être utilisé pour piloter des modèles d’entrée principaux tels que le point de vue [et la validation](gaze-and-commit.md)de la tête, ainsi que pour fournir le contexte pour les types d’interactions.</span><span class="sxs-lookup"><span data-stu-id="ba458-106">This can be used to drive primary input models such as [head gaze and commit](gaze-and-commit.md), and also to provide context for types of interactions.</span></span> <span data-ttu-id="ba458-107">Deux types de vecteurs de pointage sont disponibles par le biais de l’API: le point de regard et l’oeil de tête.</span><span class="sxs-lookup"><span data-stu-id="ba458-107">There are two types of gaze vectors available through the API: head gaze and eye gaze.</span></span>  <span data-ttu-id="ba458-108">Les deux sont fournis sous la forme d’un rayon à trois dimensions avec une origine et une direction.</span><span class="sxs-lookup"><span data-stu-id="ba458-108">Both are provided as a three dimensional ray with an origin and direction.</span></span> <span data-ttu-id="ba458-109">Les applications peuvent ensuite raycast dans leurs scènes ou dans le monde réel, et déterminer ce que l’utilisateur cible.</span><span class="sxs-lookup"><span data-stu-id="ba458-109">Applications can then raycast into their scenes, or the real world, and determine what the user is targeting.</span></span>

<span data-ttu-id="ba458-110">Le point de la **tête** représente la direction dans laquelle la tête de l’utilisateur est pointée.</span><span class="sxs-lookup"><span data-stu-id="ba458-110">**Head gaze** represents the direction that the user's head is pointed in.</span></span> <span data-ttu-id="ba458-111">Imaginez qu’il s’agit de la position et de la direction vers l’avant de l’appareil lui-même, avec la position représentant le point central entre les deux affichages.</span><span class="sxs-lookup"><span data-stu-id="ba458-111">Think of this as the position and forward direction of the device itself, with the position representing the center point between the two displays.</span></span>  <span data-ttu-id="ba458-112">Le pointage en tête est disponible sur tous les appareils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="ba458-112">Head gaze is available on all Mixed Reality devices.</span></span>

<span data-ttu-id="ba458-113">Le point de regard de l' **œil** représente la direction vers laquelle les yeux de l’utilisateur cherchent.</span><span class="sxs-lookup"><span data-stu-id="ba458-113">**Eye gaze** represents the direction that the user's eyes are looking towards.</span></span> <span data-ttu-id="ba458-114">L’origine est située entre les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ba458-114">The origin is located between the user's eyes.</span></span>  <span data-ttu-id="ba458-115">Elle est disponible sur les appareils de réalité mixte qui incluent un système de suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="ba458-115">It is available on Mixed Reality devices that include an eye tracking system.</span></span>

<span data-ttu-id="ba458-116">Les rayons de tête et de regard sont accessibles par le biais de l’API [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) .</span><span class="sxs-lookup"><span data-stu-id="ba458-116">Both head and eye gaze rays are accessible through the  [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API.</span></span> <span data-ttu-id="ba458-117">Appelez simplement [SpatialPointerPose:: TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose à l’horodatage et au [système de coordonnées](coordinate-systems-in-directx.md)spécifiés.</span><span class="sxs-lookup"><span data-stu-id="ba458-117">Simply call [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object at the specified timestamp and [coordinate system](coordinate-systems-in-directx.md).</span></span> <span data-ttu-id="ba458-118">Ce SpatialPointerPose contient une origine et une direction de pointage en tête.</span><span class="sxs-lookup"><span data-stu-id="ba458-118">This SpatialPointerPose contains a head gaze origin and direction.</span></span> <span data-ttu-id="ba458-119">Il contient également une origine et une direction de pointage oculaire si le suivi oculaire est disponible.</span><span class="sxs-lookup"><span data-stu-id="ba458-119">It also contains an eye gaze origin and direction if eye tracking is available.</span></span>

## <a name="using-head-gaze"></a><span data-ttu-id="ba458-120">Utilisation de la tête de regard</span><span class="sxs-lookup"><span data-stu-id="ba458-120">Using head gaze</span></span>

<span data-ttu-id="ba458-121">Pour accéder au point de regard de l’en-tête, commencez par appeler [SpatialPointerPose:: TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose.</span><span class="sxs-lookup"><span data-stu-id="ba458-121">To access the head gaze, start by calling  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object.</span></span> <span data-ttu-id="ba458-122">Vous devez passer les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="ba458-122">You need to pass the following parameters.</span></span>
 - <span data-ttu-id="ba458-123">[SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) qui représente le système de coordonnées souhaité pour le point de regard de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="ba458-123">A [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) that represents the desired coordinate system for the head gaze.</span></span> <span data-ttu-id="ba458-124">Elle est représentée par la variable *coordinateSystem* dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="ba458-124">This is represented by the *coordinateSystem* variable in the following code.</span></span> <span data-ttu-id="ba458-125">Pour plus d’informations, consultez notre guide de développement des [systèmes de coordonnées](coordinate-systems-in-directx.md) .</span><span class="sxs-lookup"><span data-stu-id="ba458-125">For more information, visit our [coordinate systems](coordinate-systems-in-directx.md) developer guide.</span></span>
 - <span data-ttu-id="ba458-126">[Horodateur](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) qui représente l’heure exacte de la pose demandée.</span><span class="sxs-lookup"><span data-stu-id="ba458-126">A [Timestamp](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) that represents the exact time of the head pose requested.</span></span>  <span data-ttu-id="ba458-127">En général, vous utilisez un horodatage qui correspond à l’heure à laquelle le frame actuel sera affiché.</span><span class="sxs-lookup"><span data-stu-id="ba458-127">Typically you will use a timestamp that corresponds to the time when the current frame will be displayed.</span></span> <span data-ttu-id="ba458-128">Vous pouvez obtenir cet horodateur d’affichage prédit à partir d’un objet [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) , qui est accessible via le [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe)actuel.</span><span class="sxs-lookup"><span data-stu-id="ba458-128">You can get this predicted display timestamp from a  [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) object, which is accessible through the current [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).</span></span>  <span data-ttu-id="ba458-129">Cet objet HolographicFramePrediction est représenté par la  variable de prédiction dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="ba458-129">This HolographicFramePrediction object is represented by the *prediction* variable in the following code.</span></span>

 <span data-ttu-id="ba458-130">Une fois que vous avez un SpatialPointerPose valide, la position de la tête et la direction vers l’avant sont accessibles en tant que propriétés.</span><span class="sxs-lookup"><span data-stu-id="ba458-130">Once you have a valid SpatialPointerPose, the head position and forward direction are accessible as properties.</span></span>  <span data-ttu-id="ba458-131">Le code suivant montre comment y accéder.</span><span class="sxs-lookup"><span data-stu-id="ba458-131">The following code  shows how to access them.</span></span>

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

## <a name="using-eye-gaze"></a><span data-ttu-id="ba458-132">Utilisation des yeux oculaires</span><span class="sxs-lookup"><span data-stu-id="ba458-132">Using eye gaze</span></span>

<span data-ttu-id="ba458-133">L’API regard de l’œil est très similaire à la tête de regard.</span><span class="sxs-lookup"><span data-stu-id="ba458-133">The eye gaze API is very similar to head gaze.</span></span>  <span data-ttu-id="ba458-134">Elle utilise la même API [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) , qui fournit une origine de rayon et une direction que vous pouvez raycast par rapport à votre scène.</span><span class="sxs-lookup"><span data-stu-id="ba458-134">It uses the same  [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API, which provides a ray origin and direction that you can raycast against your scene.</span></span>  <span data-ttu-id="ba458-135">La seule différence est que vous devez activer explicitement le suivi visuel avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ba458-135">The only difference is that you need to explicitly enable eye tracking before using it.</span></span> <span data-ttu-id="ba458-136">Pour ce faire, vous devez effectuer deux étapes:</span><span class="sxs-lookup"><span data-stu-id="ba458-136">For this, you need to do two steps:</span></span>
1. <span data-ttu-id="ba458-137">Demandez à l’utilisateur l’autorisation d’utiliser le suivi oculaire dans votre application.</span><span class="sxs-lookup"><span data-stu-id="ba458-137">Request user permission to use eye tracking in your app.</span></span>
2. <span data-ttu-id="ba458-138">Activez la fonctionnalité «entrée de regard» dans le manifeste de votre package.</span><span class="sxs-lookup"><span data-stu-id="ba458-138">Enable the "Gaze Input" capability in your package manifest.</span></span>

### <a name="requesting-access-to-gaze-input"></a><span data-ttu-id="ba458-139">Demande d’accès à l’entrée en regard</span><span class="sxs-lookup"><span data-stu-id="ba458-139">Requesting access to gaze input</span></span>
<span data-ttu-id="ba458-140">Lorsque votre application démarre, appelez [EyesPose:: RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) pour demander l’accès au suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="ba458-140">When your app is starting up, call [EyesPose::RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) to request access to eye tracking.</span></span> <span data-ttu-id="ba458-141">Le système demande à l’utilisateur si nécessaire et retourne [GazeInputAccessStatus:: allowed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.gazeinputaccessstatus) une fois que l’accès a été accordé.</span><span class="sxs-lookup"><span data-stu-id="ba458-141">The system will prompt the user if needed, and return [GazeInputAccessStatus::Allowed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.gazeinputaccessstatus) once access has been granted.</span></span> <span data-ttu-id="ba458-142">Il s’agit d’un appel asynchrone, ce qui nécessite un peu de gestion supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="ba458-142">This is an asynchronous call, so it requires a bit of extra management.</span></span> <span data-ttu-id="ba458-143">L’exemple suivant montre comment créer un élément std:: thread détaché pour attendre le résultat, qu’il stocke dans une variable membre appelée *m_isEyeTrackingEnabled*.</span><span class="sxs-lookup"><span data-stu-id="ba458-143">The following example spins up a detached std::thread to wait for the result, which it stores to a member variable called *m_isEyeTrackingEnabled*.</span></span>

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
<span data-ttu-id="ba458-144">Le démarrage d’un thread détaché n’est qu’une option pour gérer les appels asynchrones.</span><span class="sxs-lookup"><span data-stu-id="ba458-144">Starting a detached thread is just one option for handling async calls.</span></span>  <span data-ttu-id="ba458-145">Vous pouvez également utiliser la nouvelle fonctionnalité [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) prise en charge par C++/WinRT.</span><span class="sxs-lookup"><span data-stu-id="ba458-145">Alternatively, you could use the new [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) functionality supported by C++/WinRT.</span></span>
<span data-ttu-id="ba458-146">Voici un autre exemple de demande d’autorisation de l’utilisateur:</span><span class="sxs-lookup"><span data-stu-id="ba458-146">Here is another example for asking for user permission:</span></span>
-   <span data-ttu-id="ba458-147">EyesPose:: IsSupported () permet à l’application de déclencher la boîte de dialogue d’autorisation uniquement s’il existe un dispositif de suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="ba458-147">EyesPose::IsSupported() allows the application to trigger the permission dialog only if there is an eye tracker.</span></span>
-   <span data-ttu-id="ba458-148">GazeInputAccessStatus m_gazeInputAccessStatus; Cela permet d’éviter de relancer l’invite d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="ba458-148">GazeInputAccessStatus m_gazeInputAccessStatus; // This is to prevent popping up the permission prompt over and over again.</span></span>

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


### <a name="declaring-the-gaze-input-capability"></a><span data-ttu-id="ba458-149">Déclaration de la capacité *d’entrée en regard*</span><span class="sxs-lookup"><span data-stu-id="ba458-149">Declaring the *Gaze Input* capability</span></span>

<span data-ttu-id="ba458-150">Double-cliquez sur le fichier appxmanifest dans *Explorateur de solutions*.</span><span class="sxs-lookup"><span data-stu-id="ba458-150">Double click the appxmanifest file in *Solution Explorer*.</span></span>  <span data-ttu-id="ba458-151">Accédez ensuite à la section *fonctionnalités* et vérifiez la capacité *d’entrée de regard* .</span><span class="sxs-lookup"><span data-stu-id="ba458-151">Then navigate to the *Capabilities* section and check the *Gaze Input* capability.</span></span> 

![Capacité d’entrée en regard](images/gaze-input-capability.png)

<span data-ttu-id="ba458-153">Cela ajoute les lignes suivantes à la section *package* dans le fichier appxmanifest:</span><span class="sxs-lookup"><span data-stu-id="ba458-153">This adds the following lines to the *Package* section in the appxmanifest file:</span></span>
```xml
  <Capabilities>
    <DeviceCapability Name="gazeInput" />
  </Capabilities>
```

### <a name="getting-the-eye-gaze-ray"></a><span data-ttu-id="ba458-154">Obtenir l’œil</span><span class="sxs-lookup"><span data-stu-id="ba458-154">Getting the eye gaze ray</span></span>
<span data-ttu-id="ba458-155">Une fois que vous avez reçu l’accès à ET, vous êtes libre de prendre le regard de l’œil à chaque cadre.</span><span class="sxs-lookup"><span data-stu-id="ba458-155">Once you have received access to ET, you are free to grab the eye gaze ray every frame.</span></span>  <span data-ttu-id="ba458-156">Tout comme avec le regard de la tête, récupérez [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) en appelant [SpatialPointerPose:: TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec un horodatage et un système de coordonnées souhaités.</span><span class="sxs-lookup"><span data-stu-id="ba458-156">Just as with head gaze, get the [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) by calling [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with a desired timestamp and coordinate system.</span></span> <span data-ttu-id="ba458-157">SpatialPointerPose contient un objet [EyesPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) via la propriété [Eyes](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) .</span><span class="sxs-lookup"><span data-stu-id="ba458-157">The SpatialPointerPose contains an [EyesPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) object through the [Eyes](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) property.</span></span> <span data-ttu-id="ba458-158">Ce n’est pas NULL uniquement si le suivi oculaire est activé.</span><span class="sxs-lookup"><span data-stu-id="ba458-158">This is non-null only if eye tracking is enabled.</span></span> <span data-ttu-id="ba458-159">À partir de là, vous pouvez vérifier si l’utilisateur de l’appareil a un étalonnage de suivi oculaire en appelant [EyesPose:: IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span><span class="sxs-lookup"><span data-stu-id="ba458-159">From there you can check if the user in the device has an eye tracking calibration by calling [EyesPose::IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span></span>  <span data-ttu-id="ba458-160">Ensuite, utilisez la [propriété de](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) pointage pour obtenir le [SpatialRay](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialray) contianing la position et la direction du regard.</span><span class="sxs-lookup"><span data-stu-id="ba458-160">Next, use the [Gaze](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) property to get the a [SpatialRay](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialray) contianing the eye gaze position and direction.</span></span> <span data-ttu-id="ba458-161">La propriété de pointage peut parfois avoir la valeur null. Assurez-vous de le vérifier.</span><span class="sxs-lookup"><span data-stu-id="ba458-161">The Gaze property can sometimes be null, so be sure to check for this.</span></span> <span data-ttu-id="ba458-162">Cela peut se produire si un utilisateur calibré ferme temporairement ses yeux.</span><span class="sxs-lookup"><span data-stu-id="ba458-162">This can happen is if a calibrated user temporarily closes their eyes.</span></span>

<span data-ttu-id="ba458-163">Le code suivant montre comment accéder à l’œil-regard.</span><span class="sxs-lookup"><span data-stu-id="ba458-163">The following code shows how to access the eye gaze ray.</span></span>

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

## <a name="correlating-gaze-with-other-inputs"></a><span data-ttu-id="ba458-164">Corrélation du regard avec d’autres entrées</span><span class="sxs-lookup"><span data-stu-id="ba458-164">Correlating gaze with other inputs</span></span>

<span data-ttu-id="ba458-165">Il peut arriver que vous ayez besoin d’un [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) qui correspond à un événement dans le passé.</span><span class="sxs-lookup"><span data-stu-id="ba458-165">Sometimes you may find that you need a [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) that corresponds with an event in the past.</span></span> <span data-ttu-id="ba458-166">Par exemple, si l’utilisateur effectue un robinet d’air, votre application peut souhaiter savoir ce qu’elle recherchait.</span><span class="sxs-lookup"><span data-stu-id="ba458-166">For example, if the user performs an Air Tap, your app might want to know what they were looking at.</span></span> <span data-ttu-id="ba458-167">À cet effet, l’utilisation simple de [SpatialPointerPose:: TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec le temps de trame prédit serait inexacte en raison de la latence entre le traitement d’entrée du système et la durée d’affichage.</span><span class="sxs-lookup"><span data-stu-id="ba458-167">For this purpose, simply using [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with the predicted frame time would be inaccurate because of the latency between system input processing and display time.</span></span> <span data-ttu-id="ba458-168">En outre, si vous utilisez des regards oculaires pour le ciblage, nos yeux ont tendance à se déplacer même avant de terminer une action de validation.</span><span class="sxs-lookup"><span data-stu-id="ba458-168">In addition, if using eye gaze for targeting, our eyes tend to move on even before finishing a commit action.</span></span> <span data-ttu-id="ba458-169">Il s’agit d’un problème moins grave pour une pression aérienne simple, mais il devient plus critique lors de la combinaison de longues commandes vocales avec des mouvements d’œil rapides.</span><span class="sxs-lookup"><span data-stu-id="ba458-169">This is less of an issue for a simple Air Tap, but becomes more critical when combining long voice commands with fast eye movements.</span></span> <span data-ttu-id="ba458-170">L’une des façons de gérer ce scénario consiste à effectuer un appel supplémentaire à [SpatialPointerPose:: TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), à l’aide d’un horodateur historique qui correspond à l’événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="ba458-170">One way to handle this scenario is to make an additional call to  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), using a historical timestamp that corresponds to the input event.</span></span>  

<span data-ttu-id="ba458-171">Toutefois, pour les entrées qui acheminent le SpatialInteractionManager, il existe une méthode plus simple.</span><span class="sxs-lookup"><span data-stu-id="ba458-171">However, for input that routes through the SpatialInteractionManager, there's an easier method.</span></span> <span data-ttu-id="ba458-172">[SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) a sa propre fonction [TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) .</span><span class="sxs-lookup"><span data-stu-id="ba458-172">The [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) has its very own [TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) function.</span></span> <span data-ttu-id="ba458-173">L’appel de qui fournira un [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) parfaitement corrélé sans les deviner.</span><span class="sxs-lookup"><span data-stu-id="ba458-173">Calling that will provide a perfectly correlated [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) without the guesswork.</span></span> <span data-ttu-id="ba458-174">Pour plus d’informations sur l’utilisation de SpatialInteractionSourceStates, jetez un coup d’œil aux [contrôleurs mains et motion dans](hands-and-motion-controllers-in-directx.md) la documentation DirectX.</span><span class="sxs-lookup"><span data-stu-id="ba458-174">For more information on working with SpatialInteractionSourceStates, take a look at the [Hands and Motion Controllers in DirectX](hands-and-motion-controllers-in-directx.md) documentation.</span></span>

## <a name="see-also"></a><span data-ttu-id="ba458-175">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ba458-175">See also</span></span>
* [<span data-ttu-id="ba458-176">Modèle d’entrée de regard et de validation de tête</span><span class="sxs-lookup"><span data-stu-id="ba458-176">Head gaze and commit input model</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="ba458-177">Eye-point de regard sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="ba458-177">Eye-gaze on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="ba458-178">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="ba458-178">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
* [<span data-ttu-id="ba458-179">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="ba458-179">Voice Input in DirectX</span></span>](voice-input-in-directx.md)
* [<span data-ttu-id="ba458-180">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="ba458-180">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
