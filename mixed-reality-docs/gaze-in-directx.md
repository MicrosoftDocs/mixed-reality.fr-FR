---
title: Tête et regard de DirectX
description: Guide du développeur pour utiliser le suivi des regards et des yeux en tête dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 05/09/2019
ms.topic: article
keywords: œil-point d’intersection, suivi des têtes, suivi oculaire, DirectX, entrée, hologrammes
ms.openlocfilehash: 48188cc8c886b371847357701b42249f486bceac
ms.sourcegitcommit: 2e54d0aff91dc31aa0020c865dada3ae57ae0ffc
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2019
ms.locfileid: "73641120"
---
# <a name="head-gaze-and-eye-gaze-input-in-directx"></a><span data-ttu-id="5460e-104">Entrée en regard des points de regard et de pointage dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5460e-104">Head-gaze and eye-gaze input in DirectX</span></span>

<span data-ttu-id="5460e-105">Dans Windows Mixed Reality, l’entrée en regard de l’œil et de la tête est utilisée pour déterminer ce que l’utilisateur examine.</span><span class="sxs-lookup"><span data-stu-id="5460e-105">In Windows Mixed Reality, eye and head gaze input is used to determine what the user is looking at.</span></span> <span data-ttu-id="5460e-106">Cela peut être utilisé pour piloter des modèles d’entrée principaux tels que le [point d’interposition et la validation](gaze-and-commit.md), ainsi que pour fournir le contexte pour les types d’interactions.</span><span class="sxs-lookup"><span data-stu-id="5460e-106">This can be used to drive primary input models such as [head-gaze and commit](gaze-and-commit.md), and also to provide context for types of interactions.</span></span> <span data-ttu-id="5460e-107">Deux types de vecteurs de pointage sont disponibles par le biais de l’API : le point de regard et l’œil.</span><span class="sxs-lookup"><span data-stu-id="5460e-107">There are two types of gaze vectors available through the API: head-gaze and eye-gaze.</span></span>  <span data-ttu-id="5460e-108">Les deux sont fournis sous la forme d’un rayon à trois dimensions avec une origine et une direction.</span><span class="sxs-lookup"><span data-stu-id="5460e-108">Both are provided as a three dimensional ray with an origin and direction.</span></span> <span data-ttu-id="5460e-109">Les applications peuvent ensuite raycast dans leurs scènes ou dans le monde réel, et déterminer ce que l’utilisateur cible.</span><span class="sxs-lookup"><span data-stu-id="5460e-109">Applications can then raycast into their scenes, or the real world, and determine what the user is targeting.</span></span>

<span data-ttu-id="5460e-110">**Tête-** point de regard représente la direction dans laquelle la tête de l’utilisateur est pointée.</span><span class="sxs-lookup"><span data-stu-id="5460e-110">**Head-gaze** represents the direction that the user's head is pointed in.</span></span> <span data-ttu-id="5460e-111">Imaginez qu’il s’agit de la position et de la direction vers l’avant de l’appareil lui-même, avec la position représentant le point central entre les deux affichages.</span><span class="sxs-lookup"><span data-stu-id="5460e-111">Think of this as the position and forward direction of the device itself, with the position representing the center point between the two displays.</span></span> <span data-ttu-id="5460e-112">La tête de regard est disponible sur tous les appareils de réalité mixte.</span><span class="sxs-lookup"><span data-stu-id="5460e-112">Head-gaze is available on all Mixed Reality devices.</span></span>

<span data-ttu-id="5460e-113">**Eye-point de regard** représente la direction vers laquelle les yeux de l’utilisateur cherchent.</span><span class="sxs-lookup"><span data-stu-id="5460e-113">**Eye-gaze** represents the direction that the user's eyes are looking towards.</span></span> <span data-ttu-id="5460e-114">L’origine est située entre les yeux de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5460e-114">The origin is located between the user's eyes.</span></span>  <span data-ttu-id="5460e-115">Elle est disponible sur les appareils de réalité mixte qui incluent un système de suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="5460e-115">It is available on Mixed Reality devices that include an eye tracking system.</span></span>

<span data-ttu-id="5460e-116">Les rayons de tête et de regard sont accessibles par le biais de l’API [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) .</span><span class="sxs-lookup"><span data-stu-id="5460e-116">Both head and eye-gaze rays are accessible through the  [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API.</span></span> <span data-ttu-id="5460e-117">Appelez simplement [SpatialPointerPose :: TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose à l’horodatage et au [système de coordonnées](coordinate-systems-in-directx.md)spécifiés.</span><span class="sxs-lookup"><span data-stu-id="5460e-117">Simply call [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object at the specified timestamp and [coordinate system](coordinate-systems-in-directx.md).</span></span> <span data-ttu-id="5460e-118">Ce SpatialPointerPose contient une origine et une direction de pointage.</span><span class="sxs-lookup"><span data-stu-id="5460e-118">This SpatialPointerPose contains a head-gaze origin and direction.</span></span> <span data-ttu-id="5460e-119">Elle contient également un point d’origine et une direction de regard si le suivi oculaire est disponible.</span><span class="sxs-lookup"><span data-stu-id="5460e-119">It also contains an eye-gaze origin and direction if eye tracking is available.</span></span>

### <a name="device-support"></a><span data-ttu-id="5460e-120">Périphériques pris en charge</span><span class="sxs-lookup"><span data-stu-id="5460e-120">Device support</span></span>
<table>
<colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
</colgroup>
<tr>
     <td><span data-ttu-id="5460e-121"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="5460e-121"><strong>Feature</strong></span></span></td>
     <td><span data-ttu-id="5460e-122"><a href="hololens-hardware-details.md"><strong>HoloLens (1ère génération)</strong></a></span><span class="sxs-lookup"><span data-stu-id="5460e-122"><a href="hololens-hardware-details.md"><strong>HoloLens (1st gen)</strong></a></span></span></td>
     <td><span data-ttu-id="5460e-123"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span><span class="sxs-lookup"><span data-stu-id="5460e-123"><a href="https://docs.microsoft.com/hololens/hololens2-hardware"><strong>HoloLens 2</strong></span></span></td>
     <td><span data-ttu-id="5460e-124"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="5460e-124"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
</tr>
<tr>
     <td><span data-ttu-id="5460e-125">Suivi de la tête</span><span class="sxs-lookup"><span data-stu-id="5460e-125">Head-gaze</span></span></td>
     <td><span data-ttu-id="5460e-126">✔️</span><span class="sxs-lookup"><span data-stu-id="5460e-126">✔️</span></span></td>
     <td><span data-ttu-id="5460e-127">✔️</span><span class="sxs-lookup"><span data-stu-id="5460e-127">✔️</span></span></td>
     <td><span data-ttu-id="5460e-128">✔️</span><span class="sxs-lookup"><span data-stu-id="5460e-128">✔️</span></span></td>
</tr>
<tr>
     <td><span data-ttu-id="5460e-129">Œil-point de regard</span><span class="sxs-lookup"><span data-stu-id="5460e-129">Eye-gaze</span></span></td>
     <td>❌</td>
     <td><span data-ttu-id="5460e-130">✔️</span><span class="sxs-lookup"><span data-stu-id="5460e-130">✔️</span></span></td>
     <td>❌</td>
</tr>
</table>

## <a name="using-head-gaze"></a><span data-ttu-id="5460e-131">Utilisation de l’en-tête</span><span class="sxs-lookup"><span data-stu-id="5460e-131">Using head-gaze</span></span>

<span data-ttu-id="5460e-132">Pour accéder au point de regard, commencez par appeler [SpatialPointerPose :: TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose.</span><span class="sxs-lookup"><span data-stu-id="5460e-132">To access the head-gaze, start by calling  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) to receive a new SpatialPointerPose object.</span></span> <span data-ttu-id="5460e-133">Vous devez passer les paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="5460e-133">You need to pass the following parameters.</span></span>
 - <span data-ttu-id="5460e-134">[SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) qui représente le système de coordonnées souhaité pour le point de regard de début.</span><span class="sxs-lookup"><span data-stu-id="5460e-134">A [SpatialCoordinateSystem](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialcoordinatesystem) that represents the desired coordinate system for the head-gaze.</span></span> <span data-ttu-id="5460e-135">Elle est représentée par la variable *coordinateSystem* dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="5460e-135">This is represented by the *coordinateSystem* variable in the following code.</span></span> <span data-ttu-id="5460e-136">Pour plus d’informations, consultez notre guide de développement des [systèmes de coordonnées](coordinate-systems-in-directx.md) .</span><span class="sxs-lookup"><span data-stu-id="5460e-136">For more information, visit our [coordinate systems](coordinate-systems-in-directx.md) developer guide.</span></span>
 - <span data-ttu-id="5460e-137">[Horodateur](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) qui représente l’heure exacte de la pose demandée.</span><span class="sxs-lookup"><span data-stu-id="5460e-137">A [Timestamp](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) that represents the exact time of the head pose requested.</span></span>  <span data-ttu-id="5460e-138">En général, vous utilisez un horodatage qui correspond à l’heure à laquelle le frame actuel sera affiché.</span><span class="sxs-lookup"><span data-stu-id="5460e-138">Typically you will use a timestamp that corresponds to the time when the current frame will be displayed.</span></span> <span data-ttu-id="5460e-139">Vous pouvez obtenir cet horodateur d’affichage prédit à partir d’un objet [HolographicFramePrediction](https://docs.microsoft.com//uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) , qui est accessible via le [HolographicFrame](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe)actuel.</span><span class="sxs-lookup"><span data-stu-id="5460e-139">You can get this predicted display timestamp from a  [HolographicFramePrediction](https://docs.microsoft.com//uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) object, which is accessible through the current [HolographicFrame](https://docs.microsoft.com//uwp/api/windows.graphics.holographic.holographicframe).</span></span>  <span data-ttu-id="5460e-140">Cet objet HolographicFramePrediction est représenté par la variable de *prédiction* dans le code suivant.</span><span class="sxs-lookup"><span data-stu-id="5460e-140">This HolographicFramePrediction object is represented by the *prediction* variable in the following code.</span></span>

 <span data-ttu-id="5460e-141">Une fois que vous avez un SpatialPointerPose valide, la position de la tête et la direction vers l’avant sont accessibles en tant que propriétés.</span><span class="sxs-lookup"><span data-stu-id="5460e-141">Once you have a valid SpatialPointerPose, the head position and forward direction are accessible as properties.</span></span>  <span data-ttu-id="5460e-142">Le code suivant montre comment y accéder.</span><span class="sxs-lookup"><span data-stu-id="5460e-142">The following code  shows how to access them.</span></span>

 ```cpp
using namespace winrt::Windows::UI::Input::Spatial;
using namespace winrt::Windows::Foundation::Numerics;

SpatialPointerPose pointerPose = SpatialPointerPose::TryGetAtTimestamp(coordinateSystem, prediction.Timestamp());
if (pointerPose)
{
    float3 headPosition = pointerPose.Head().Position();
    float3 headForwardDirection = pointerPose.Head().ForwardDirection();

    // Do something with the head-gaze
}
```

## <a name="using-eye-gaze"></a><span data-ttu-id="5460e-143">Utilisation des yeux</span><span class="sxs-lookup"><span data-stu-id="5460e-143">Using eye-gaze</span></span>

<span data-ttu-id="5460e-144">Veuillez noter que pour que vos utilisateurs utilisent une entrée en regard de l’œil, chaque utilisateur doit passer par un étalonnage de l' [utilisateur de suivi oculaire](calibration.md) la première fois qu’il utilise l’appareil.</span><span class="sxs-lookup"><span data-stu-id="5460e-144">Please note that for your users to use eye-gaze input, each user has to go through an [eye tracking user calibration](calibration.md) the first time they use the device.</span></span> <span data-ttu-id="5460e-145">L’API Eye-regard est très similaire à la tête de regard.</span><span class="sxs-lookup"><span data-stu-id="5460e-145">The eye-gaze API is very similar to head-gaze.</span></span>
<span data-ttu-id="5460e-146">Elle utilise la même API [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) , qui fournit une origine de rayon et une direction que vous pouvez raycast par rapport à votre scène.</span><span class="sxs-lookup"><span data-stu-id="5460e-146">It uses the same [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API, which provides a ray origin and direction that you can raycast against your scene.</span></span>  <span data-ttu-id="5460e-147">La seule différence est que vous devez activer explicitement le suivi visuel avant de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="5460e-147">The only difference is that you need to explicitly enable eye tracking before using it.</span></span> <span data-ttu-id="5460e-148">Pour ce faire, vous devez effectuer deux étapes :</span><span class="sxs-lookup"><span data-stu-id="5460e-148">For this, you need to do two steps:</span></span>
1. <span data-ttu-id="5460e-149">Demandez à l’utilisateur l’autorisation d’utiliser le suivi oculaire dans votre application.</span><span class="sxs-lookup"><span data-stu-id="5460e-149">Request user permission to use eye tracking in your app.</span></span>
2. <span data-ttu-id="5460e-150">Activez la fonctionnalité « entrée de regard » dans le manifeste de votre package.</span><span class="sxs-lookup"><span data-stu-id="5460e-150">Enable the "Gaze Input" capability in your package manifest.</span></span>

### <a name="requesting-access-to-eye-gaze-input"></a><span data-ttu-id="5460e-151">Demande d’accès à une entrée en regard des yeux</span><span class="sxs-lookup"><span data-stu-id="5460e-151">Requesting access to eye-gaze input</span></span>
<span data-ttu-id="5460e-152">Lorsque votre application démarre, appelez [EyesPose :: RequestAccessAsync](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) pour demander l’accès au suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="5460e-152">When your app is starting up, call [EyesPose::RequestAccessAsync](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) to request access to eye tracking.</span></span> <span data-ttu-id="5460e-153">Le système demande à l’utilisateur si nécessaire et retourne [GazeInputAccessStatus :: allowed](https://docs.microsoft.com//uwp/api/windows.ui.input.gazeinputaccessstatus) une fois que l’accès a été accordé.</span><span class="sxs-lookup"><span data-stu-id="5460e-153">The system will prompt the user if needed, and return [GazeInputAccessStatus::Allowed](https://docs.microsoft.com//uwp/api/windows.ui.input.gazeinputaccessstatus) once access has been granted.</span></span> <span data-ttu-id="5460e-154">Il s’agit d’un appel asynchrone, ce qui nécessite un peu de gestion supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="5460e-154">This is an asynchronous call, so it requires a bit of extra management.</span></span> <span data-ttu-id="5460e-155">L’exemple suivant montre comment créer un élément std :: thread détaché pour attendre le résultat, qu’il stocke dans une variable membre appelée *m_isEyeTrackingEnabled*.</span><span class="sxs-lookup"><span data-stu-id="5460e-155">The following example spins up a detached std::thread to wait for the result, which it stores to a member variable called *m_isEyeTrackingEnabled*.</span></span>

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
<span data-ttu-id="5460e-156">Le démarrage d’un thread détaché n’est qu’une option pour gérer les appels asynchrones.</span><span class="sxs-lookup"><span data-stu-id="5460e-156">Starting a detached thread is just one option for handling async calls.</span></span> <span data-ttu-id="5460e-157">Vous pouvez également utiliser la nouvelle fonctionnalité [co_await](https://docs.microsoft.com//windows/uwp/cpp-and-winrt-apis/concurrency) prise en charge par C++/WinRT.</span><span class="sxs-lookup"><span data-stu-id="5460e-157">Alternatively, you could use the new [co_await](https://docs.microsoft.com//windows/uwp/cpp-and-winrt-apis/concurrency) functionality supported by C++/WinRT.</span></span>
<span data-ttu-id="5460e-158">Voici un autre exemple de demande d’autorisation de l’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="5460e-158">Here is another example for asking for user permission:</span></span>
-   <span data-ttu-id="5460e-159">EyesPose :: IsSupported () permet à l’application de déclencher la boîte de dialogue d’autorisation uniquement s’il existe un dispositif de suivi oculaire.</span><span class="sxs-lookup"><span data-stu-id="5460e-159">EyesPose::IsSupported() allows the application to trigger the permission dialog only if there is an eye tracker.</span></span>
-   <span data-ttu-id="5460e-160">GazeInputAccessStatus m_gazeInputAccessStatus; Cela permet d’éviter de relancer l’invite d’autorisation.</span><span class="sxs-lookup"><span data-stu-id="5460e-160">GazeInputAccessStatus m_gazeInputAccessStatus; // This is to prevent popping up the permission prompt over and over again.</span></span>

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

### <a name="declaring-the-gaze-input-capability"></a><span data-ttu-id="5460e-161">Déclaration de la capacité *d’entrée en regard*</span><span class="sxs-lookup"><span data-stu-id="5460e-161">Declaring the *Gaze Input* capability</span></span>

<span data-ttu-id="5460e-162">Double-cliquez sur le fichier appxmanifest dans *Explorateur de solutions*.</span><span class="sxs-lookup"><span data-stu-id="5460e-162">Double click the appxmanifest file in *Solution Explorer*.</span></span>  <span data-ttu-id="5460e-163">Accédez ensuite à la section *fonctionnalités* et vérifiez la capacité *d’entrée de regard* .</span><span class="sxs-lookup"><span data-stu-id="5460e-163">Then navigate to the *Capabilities* section and check the *Gaze Input* capability.</span></span> 

![Capacité d’entrée en regard](images/gaze-input-capability.png)

<span data-ttu-id="5460e-165">Cela ajoute les lignes suivantes à la section *package* dans le fichier appxmanifest :</span><span class="sxs-lookup"><span data-stu-id="5460e-165">This adds the following lines to the *Package* section in the appxmanifest file:</span></span>
```xml
  <Capabilities>
    <DeviceCapability Name="gazeInput" />
  </Capabilities>
```

### <a name="getting-the-eye-gaze-ray"></a><span data-ttu-id="5460e-166">Obtenir le regard de l’œil</span><span class="sxs-lookup"><span data-stu-id="5460e-166">Getting the eye-gaze ray</span></span>
<span data-ttu-id="5460e-167">Une fois que vous avez reçu l’accès à ET, vous êtes libre de prendre le regard de chaque image.</span><span class="sxs-lookup"><span data-stu-id="5460e-167">Once you have received access to ET, you are free to grab the eye-gaze ray every frame.</span></span>
<span data-ttu-id="5460e-168">Tout comme avec le regard de tête, récupérez [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) en appelant [SpatialPointerPose :: TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec un horodatage et un système de coordonnées souhaités.</span><span class="sxs-lookup"><span data-stu-id="5460e-168">Just as with head-gaze, get the [SpatialPointerPose](https://docs.microsoft.com//uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) by calling [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with a desired timestamp and coordinate system.</span></span> <span data-ttu-id="5460e-169">SpatialPointerPose contient un objet [EyesPose](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose) via la propriété [Eyes](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) .</span><span class="sxs-lookup"><span data-stu-id="5460e-169">The SpatialPointerPose contains an [EyesPose](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose) object through the [Eyes](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) property.</span></span> <span data-ttu-id="5460e-170">Ce n’est pas NULL uniquement si le suivi oculaire est activé.</span><span class="sxs-lookup"><span data-stu-id="5460e-170">This is non-null only if eye tracking is enabled.</span></span> <span data-ttu-id="5460e-171">À partir de là, vous pouvez vérifier si l’utilisateur de l’appareil a un étalonnage de suivi oculaire en appelant [EyesPose :: IsCalibrationValid](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span><span class="sxs-lookup"><span data-stu-id="5460e-171">From there you can check if the user in the device has an eye tracking calibration by calling [EyesPose::IsCalibrationValid](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).</span></span>  <span data-ttu-id="5460e-172">Ensuite, utilisez la [propriété de](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) pointage pour obtenir le [SpatialRay](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialray) contianing la position et la direction de l’oeil.</span><span class="sxs-lookup"><span data-stu-id="5460e-172">Next, use the [Gaze](https://docs.microsoft.com//uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) property to get the a [SpatialRay](https://docs.microsoft.com//uwp/api/windows.perception.spatial.spatialray) contianing the eye-gaze position and direction.</span></span> <span data-ttu-id="5460e-173">La propriété de pointage peut parfois avoir la valeur null. Assurez-vous de le vérifier.</span><span class="sxs-lookup"><span data-stu-id="5460e-173">The Gaze property can sometimes be null, so be sure to check for this.</span></span> <span data-ttu-id="5460e-174">Cela peut se produire si un utilisateur calibré ferme temporairement ses yeux.</span><span class="sxs-lookup"><span data-stu-id="5460e-174">This can happen is if a calibrated user temporarily closes their eyes.</span></span>

<span data-ttu-id="5460e-175">L’exemple de code suivant montre comment accéder à l’œil-regard.</span><span class="sxs-lookup"><span data-stu-id="5460e-175">The following code shows how to access the eye-gaze ray.</span></span>

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
            
            // Do something with the eye-gaze
        }
    }
}

```

## <a name="fallback-when-eye-tracking-is-not-available"></a><span data-ttu-id="5460e-176">Secours lorsque le suivi oculaire n’est pas disponible</span><span class="sxs-lookup"><span data-stu-id="5460e-176">Fallback when eye tracking is not available</span></span>
<span data-ttu-id="5460e-177">Comme mentionné dans nos [documents sur la conception des suivis oculaires](eye-tracking.md#fallback-solutions-when-eye-tracking-is-not-available), les concepteurs et les développeurs doivent savoir qu’il peut y avoir des instances dans lesquelles les données de suivi visuel peuvent ne pas être disponibles pour votre application.</span><span class="sxs-lookup"><span data-stu-id="5460e-177">As mentioned in our [eye tracking design docs](eye-tracking.md#fallback-solutions-when-eye-tracking-is-not-available), both designers as well as developers should be aware that there may be instances in which eye tracking data may not be available to your app.</span></span>
<span data-ttu-id="5460e-178">Il existe plusieurs raisons pour cela, qu’il s’agisse d’un utilisateur qui n’est pas étalonné, que l’utilisateur ait refusé à l’application d’accéder à ses données de suivi visuel ou simplement à des interférences temporaires (telles que les taches sur le Visor ou les cheveux qui boucher les yeux de l’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="5460e-178">There are various reasons for this ranging from a user not being calibrated, the user having denied the app access to his/her eye tracking data or simply temporary interferences (such as smudges on the HoloLens visor or hair occluding the user's eyes).</span></span> <span data-ttu-id="5460e-179">Alors que certaines API ont déjà été mentionnées dans ce document, nous fournissons un résumé de la façon de détecter que le suivi oculaire est disponible en tant que référence rapide :</span><span class="sxs-lookup"><span data-stu-id="5460e-179">While some of the APIs have already been mentioned in this document, in the following, we provide a summary of how to detect that eye tracking is available as a quick reference:</span></span> 

* <span data-ttu-id="5460e-180">Vérifiez que le système prend en charge le suivi visuel.</span><span class="sxs-lookup"><span data-stu-id="5460e-180">Check that the system supports eye tracking at all.</span></span> <span data-ttu-id="5460e-181">Appelez la *méthode*suivante : [Windows. perception. People. EyesPose. IsSupported ()](https://docs.microsoft.com/uwp/api/windows.perception.people.eyespose.issupported#Windows_Perception_People_EyesPose_IsSupported)</span><span class="sxs-lookup"><span data-stu-id="5460e-181">Call the following *method*: [Windows.Perception.People.EyesPose.IsSupported()](https://docs.microsoft.com/uwp/api/windows.perception.people.eyespose.issupported#Windows_Perception_People_EyesPose_IsSupported)</span></span>

* <span data-ttu-id="5460e-182">Vérifiez que l’utilisateur est étalonné.</span><span class="sxs-lookup"><span data-stu-id="5460e-182">Check that the user is calibrated.</span></span> <span data-ttu-id="5460e-183">Appelez la *propriété*suivante : [Windows. perception. People. EyesPose. IsCalibrationValid](https://docs.microsoft.com/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid)</span><span class="sxs-lookup"><span data-stu-id="5460e-183">Call the following *property*: [Windows.Perception.People.EyesPose.IsCalibrationValid](https://docs.microsoft.com/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid)</span></span> 

* <span data-ttu-id="5460e-184">Vérifiez que l’utilisateur a donné à votre application l’autorisation d’utiliser ses données de suivi oculaire : récupérez le _« GazeInputAccessStatus »_ actuel.</span><span class="sxs-lookup"><span data-stu-id="5460e-184">Check that the user has given your app permission to use their eye tracking data: Retrieve the current _'GazeInputAccessStatus'_.</span></span> <span data-ttu-id="5460e-185">Vous trouverez un exemple de la procédure à suivre pour [demander l’accès aux entrées de regard](https://docs.microsoft.com/windows/mixed-reality/gaze-in-directX#requesting-access-to-gaze-input).</span><span class="sxs-lookup"><span data-stu-id="5460e-185">An example on how to do this is explained at [Requesting access to gaze input](https://docs.microsoft.com/windows/mixed-reality/gaze-in-directX#requesting-access-to-gaze-input).</span></span>   

<span data-ttu-id="5460e-186">En outre, vous souhaiterez peut-être vérifier que vos données de suivi oculaire ne sont pas obsolètes en ajoutant un délai d’expiration entre les mises à jour reçues des données de suivi oculaire et en configurant le point de vue dans le point de vue ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="5460e-186">In addition, you may want to check that your eye tracking data is not stale by adding a timeout between received eye tracking data updates and otherwise fallback to head-gaze as discussed below.</span></span>  
<span data-ttu-id="5460e-187">Pour plus d’informations, consultez les [considérations relatives](eye-tracking.md#fallback-solutions-when-eye-tracking-is-not-available) à la conception de secours.</span><span class="sxs-lookup"><span data-stu-id="5460e-187">Please visit our [fallback design considerations](eye-tracking.md#fallback-solutions-when-eye-tracking-is-not-available) for more information.</span></span>

<br>

## <a name="correlating-gaze-with-other-inputs"></a><span data-ttu-id="5460e-188">Corrélation du regard avec d’autres entrées</span><span class="sxs-lookup"><span data-stu-id="5460e-188">Correlating gaze with other inputs</span></span>
<span data-ttu-id="5460e-189">Il peut arriver que vous ayez besoin d’un [SpatialPointerPose](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose) qui correspond à un événement dans le passé.</span><span class="sxs-lookup"><span data-stu-id="5460e-189">Sometimes you may find that you need a [SpatialPointerPose](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose) that corresponds with an event in the past.</span></span> <span data-ttu-id="5460e-190">Par exemple, si l’utilisateur effectue un robinet d’air, votre application peut souhaiter savoir ce qu’elle recherchait.</span><span class="sxs-lookup"><span data-stu-id="5460e-190">For example, if the user performs an Air Tap, your app might want to know what they were looking at.</span></span> <span data-ttu-id="5460e-191">À cet effet, l’utilisation simple de [SpatialPointerPose :: TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec le temps de trame prédit serait inexacte en raison de la latence entre le traitement d’entrée du système et la durée d’affichage.</span><span class="sxs-lookup"><span data-stu-id="5460e-191">For this purpose, simply using [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) with the predicted frame time would be inaccurate because of the latency between system input processing and display time.</span></span> <span data-ttu-id="5460e-192">En outre, si vous utilisez des yeux pour le ciblage, nos yeux ont tendance à se déplacer même avant de terminer une action de validation.</span><span class="sxs-lookup"><span data-stu-id="5460e-192">In addition, if using eye-gaze for targeting, our eyes tend to move on even before finishing a commit action.</span></span> <span data-ttu-id="5460e-193">Il s’agit d’un problème moins grave pour une pression aérienne simple, mais il devient plus critique lors de la combinaison de longues commandes vocales avec des mouvements d’œil rapides.</span><span class="sxs-lookup"><span data-stu-id="5460e-193">This is less of an issue for a simple Air Tap, but becomes more critical when combining long voice commands with fast eye movements.</span></span> <span data-ttu-id="5460e-194">L’une des façons de gérer ce scénario consiste à effectuer un appel supplémentaire à [SpatialPointerPose :: TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), à l’aide d’un horodateur historique qui correspond à l’événement d’entrée.</span><span class="sxs-lookup"><span data-stu-id="5460e-194">One way to handle this scenario is to make an additional call to  [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), using a historical timestamp that corresponds to the input event.</span></span>  

<span data-ttu-id="5460e-195">Toutefois, pour les entrées qui acheminent le SpatialInteractionManager, il existe une méthode plus simple.</span><span class="sxs-lookup"><span data-stu-id="5460e-195">However, for input that routes through the SpatialInteractionManager, there's an easier method.</span></span> <span data-ttu-id="5460e-196">[SpatialInteractionSourceState](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) a sa propre fonction [TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) .</span><span class="sxs-lookup"><span data-stu-id="5460e-196">The [SpatialInteractionSourceState](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) has its very own [TryGetAtTimestamp](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) function.</span></span> <span data-ttu-id="5460e-197">L’appel de qui fournira un [SpatialPointerPose](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose) parfaitement corrélé sans les deviner.</span><span class="sxs-lookup"><span data-stu-id="5460e-197">Calling that will provide a perfectly correlated [SpatialPointerPose](https://docs.microsoft.com//uwp/api/windows.ui.input.spatial.spatialpointerpose) without the guesswork.</span></span> <span data-ttu-id="5460e-198">Pour plus d’informations sur l’utilisation de SpatialInteractionSourceStates, jetez un coup d’œil aux [contrôleurs mains et motion dans](hands-and-motion-controllers-in-directx.md) la documentation DirectX.</span><span class="sxs-lookup"><span data-stu-id="5460e-198">For more information on working with SpatialInteractionSourceStates, take a look at the [Hands and Motion Controllers in DirectX](hands-and-motion-controllers-in-directx.md) documentation.</span></span>

<br>

## <a name="calibration"></a><span data-ttu-id="5460e-199">Auto</span><span class="sxs-lookup"><span data-stu-id="5460e-199">Calibration</span></span>
<span data-ttu-id="5460e-200">Pour que le suivi des yeux fonctionne correctement, chaque utilisateur doit passer par un étalonnage de l' [utilisateur de suivi oculaire](calibration.md).</span><span class="sxs-lookup"><span data-stu-id="5460e-200">For eye tracking to work accurately, each user is required to go through an [eye tracking user calibration](calibration.md).</span></span> <span data-ttu-id="5460e-201">Cela permet à l’appareil d’ajuster le système pour une expérience d’affichage plus confortable et de meilleure qualité pour l’utilisateur et pour garantir un suivi visuel précis en même temps.</span><span class="sxs-lookup"><span data-stu-id="5460e-201">This allows the device to adjust the system for a more comfortable and higher quality viewing experience for the user and to ensure accurate eye tracking at the same time.</span></span> <span data-ttu-id="5460e-202">Les développeurs n’ont rien à faire à leur bout pour gérer l’étalonnage de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5460e-202">Developers don’t need to do anything on their end to manage user calibration.</span></span> <span data-ttu-id="5460e-203">Le système s’assure que l’utilisateur est invité à étalonner l’appareil dans les circonstances suivantes : \* l’utilisateur utilise l’appareil pour la première fois \* l’utilisateur a opté pour le processus d’étalonnage \* le processus d’étalonnage a échoué le dernier heure à laquelle l’utilisateur a utilisé l’appareil</span><span class="sxs-lookup"><span data-stu-id="5460e-203">The system will ensure that the user gets prompted to calibrate the device under the following circumstances: \*The user is using the device for the first time \*The user previously opted out of the calibration process \*The calibration process did not succeed the last time the user used the device</span></span>

<span data-ttu-id="5460e-204">Les développeurs doivent veiller à fournir une prise en charge adéquate pour les utilisateurs pour lesquels les données de suivi oculaire peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="5460e-204">Developers should make sure to provide adequate support for users for whom eye tracking data may not be available.</span></span> <span data-ttu-id="5460e-205">En savoir plus sur les considérations relatives aux solutions de secours au [suivi oculaire sur Hololens 2](eye-tracking.md).</span><span class="sxs-lookup"><span data-stu-id="5460e-205">Learn more about considerations for fallback solutions at [Eye tracking on Hololens 2](eye-tracking.md).</span></span>

<br>

## <a name="see-also"></a><span data-ttu-id="5460e-206">Articles associés</span><span class="sxs-lookup"><span data-stu-id="5460e-206">See also</span></span>
* [<span data-ttu-id="5460e-207">Étalonnage</span><span class="sxs-lookup"><span data-stu-id="5460e-207">Calibration</span></span>](calibration.md)
* [<span data-ttu-id="5460e-208">Systèmes de coordonnées dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5460e-208">Coordinate systems in DirectX</span></span>](coordinate-systems-in-directx.md)
* [<span data-ttu-id="5460e-209">Eye-point de regard sur HoloLens 2</span><span class="sxs-lookup"><span data-stu-id="5460e-209">Eye-gaze on HoloLens 2</span></span>](eye-tracking.md)
* [<span data-ttu-id="5460e-210">Modèle d’entrée de regard et de validation</span><span class="sxs-lookup"><span data-stu-id="5460e-210">Gaze and commit input model</span></span>](gaze-and-commit.md)
* [<span data-ttu-id="5460e-211">Mains et contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5460e-211">Hands and motion controllers in DirectX</span></span>](hands-and-motion-controllers-in-directx.md)
* [<span data-ttu-id="5460e-212">Entrée vocale dans DirectX</span><span class="sxs-lookup"><span data-stu-id="5460e-212">Voice Input in DirectX</span></span>](voice-input-in-directx.md)
