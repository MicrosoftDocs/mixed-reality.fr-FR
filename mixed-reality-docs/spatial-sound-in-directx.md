---
title: Son spatial dans DirectX
description: Ajoutez son spatial à vos applications de réalité mixte Windows basées sur DirectX en utilisant les bibliothèques audio XAudio2 et xAPO.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows mixtes réalité, son spatial, applications, XAudio2, de bas niveau, xAPO, bibliothèque audio, procédure pas à pas, DirectX
ms.openlocfilehash: 04d8c43ab400eed4cec5cbd848af5b888cb66e4b
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597141"
---
# <a name="spatial-sound-in-directx"></a><span data-ttu-id="c30af-104">Son spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="c30af-104">Spatial sound in DirectX</span></span>

<span data-ttu-id="c30af-105">Ajouter du son spatial à vos applications de réalité mixte Windows basées sur DirectX à l’aide de la [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049.aspx) et [xAPO](https://msdn.microsoft.com/library/windows/desktop/ee415735.aspx) bibliothèques audio.</span><span class="sxs-lookup"><span data-stu-id="c30af-105">Add spatial sound to your Windows Mixed Reality apps based on DirectX by using the [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049.aspx) and [xAPO](https://msdn.microsoft.com/library/windows/desktop/ee415735.aspx) audio libraries.</span></span>

<span data-ttu-id="c30af-106">Cette rubrique utilise l’exemple de code à partir de la HolographicHRTFAudioSample.</span><span class="sxs-lookup"><span data-stu-id="c30af-106">This topic uses sample code from the HolographicHRTFAudioSample.</span></span>

>[!NOTE]
><span data-ttu-id="c30af-107">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="c30af-107">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="c30af-108">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="c30af-108">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="overview-of-head-relative-spatial-sound"></a><span data-ttu-id="c30af-109">Vue d’ensemble de son Spatial relatif</span><span class="sxs-lookup"><span data-stu-id="c30af-109">Overview of Head Relative Spatial Sound</span></span>

<span data-ttu-id="c30af-110">Son spatial est implémenté comme un **objet de traitement audio (APO)** qui utilise un **tête liés à la fonction de transfert (HRTF)** filtrer pour *spatialize* un flux audio ordinaire.</span><span class="sxs-lookup"><span data-stu-id="c30af-110">Spatial sound is implemented as an **audio processing object (APO)** that uses a **head related transfer function (HRTF)** filter to *spatialize* an ordinary audio stream.</span></span>

<span data-ttu-id="c30af-111">Inclure ces fichiers d’en-tête dans pch.h pour accéder à l’API audio :</span><span class="sxs-lookup"><span data-stu-id="c30af-111">Include these header files in pch.h to access the audio APIs:</span></span>
* <span data-ttu-id="c30af-112">XAudio2.h</span><span class="sxs-lookup"><span data-stu-id="c30af-112">XAudio2.h</span></span>
* <span data-ttu-id="c30af-113">xapo.h</span><span class="sxs-lookup"><span data-stu-id="c30af-113">xapo.h</span></span>
* <span data-ttu-id="c30af-114">hrtfapoapi.h</span><span class="sxs-lookup"><span data-stu-id="c30af-114">hrtfapoapi.h</span></span>

<span data-ttu-id="c30af-115">Pour configurer son spatial :</span><span class="sxs-lookup"><span data-stu-id="c30af-115">To set up spatial sound:</span></span>
1. <span data-ttu-id="c30af-116">Appelez [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) pour initialiser une nouvelle APO pour l’audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="c30af-116">Call [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) to initialize a new APO for HRTF audio.</span></span>
2. <span data-ttu-id="c30af-117">Affecter le [les paramètres HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186608.aspx) et [environnement de HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186604.aspx) pour définir les caractéristiques acoustiques de la APO son spatial.</span><span class="sxs-lookup"><span data-stu-id="c30af-117">Assign the [HRTF parameters](https://msdn.microsoft.com/library/windows/desktop/mt186608.aspx) and [HRTF environment](https://msdn.microsoft.com/library/windows/desktop/mt186604.aspx) to define the acoustic characteristics of the spatial sound APO.</span></span>
3. <span data-ttu-id="c30af-118">Configurer le moteur XAudio2 pour le traitement de HRTF.</span><span class="sxs-lookup"><span data-stu-id="c30af-118">Set up the XAudio2 engine for HRTF processing.</span></span>
4. <span data-ttu-id="c30af-119">Créer un [IXAudio2SourceVoice](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.aspx) objet et appelez [Démarrer](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx).</span><span class="sxs-lookup"><span data-stu-id="c30af-119">Create an [IXAudio2SourceVoice](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.aspx) object and call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx).</span></span>

## <a name="implementing-hrtf-and-spatial-sound-in-your-directx-app"></a><span data-ttu-id="c30af-120">Implémentation de HRTF et son spatial dans votre application DirectX</span><span class="sxs-lookup"><span data-stu-id="c30af-120">Implementing HRTF and spatial sound in your DirectX app</span></span>

<span data-ttu-id="c30af-121">Vous pouvez obtenir divers effets en configurant le APO HRTF avec des environnements et des paramètres différents.</span><span class="sxs-lookup"><span data-stu-id="c30af-121">You can achieve a variety of effects by configuring the HRTF APO with different parameters and environments.</span></span> <span data-ttu-id="c30af-122">Utilisez le code suivant pour Explorer les possibilités.</span><span class="sxs-lookup"><span data-stu-id="c30af-122">Use the following code to explore the possibilities.</span></span> <span data-ttu-id="c30af-123">Télécharger l’exemple de code de plateforme Windows universelle à partir d’ici : [Exemple de son spatial](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpatialSound)</span><span class="sxs-lookup"><span data-stu-id="c30af-123">Download the Universal Windows Platform code sample from here: [Spatial sound sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpatialSound)</span></span>

<span data-ttu-id="c30af-124">Types d’assistance sont disponibles dans ces fichiers :</span><span class="sxs-lookup"><span data-stu-id="c30af-124">Helper types are available in these files:</span></span>
* <span data-ttu-id="c30af-125">[AudioFileReader.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/AudioFileReader.cpp): Charge les fichiers audio à l’aide de Media Foundation et le [IMFSourceReader interface](https://msdn.microsoft.com/library/windows/desktop/dd374655.aspx).</span><span class="sxs-lookup"><span data-stu-id="c30af-125">[AudioFileReader.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/AudioFileReader.cpp): Loads audio files by using Media Foundation and the [IMFSourceReader interface](https://msdn.microsoft.com/library/windows/desktop/dd374655.aspx).</span></span>
* <span data-ttu-id="c30af-126">[XAudio2Helpers.h](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/XAudio2Helpers.h): Implémente le **SetupXAudio2** fonction pour initialiser XAudio2 pour le traitement de HRTF.</span><span class="sxs-lookup"><span data-stu-id="c30af-126">[XAudio2Helpers.h](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/XAudio2Helpers.h): Implements the **SetupXAudio2** function to initialize XAudio2 for HRTF processing.</span></span>

### <a name="add-spatial-sound-for-an-omnidirectional-source"></a><span data-ttu-id="c30af-127">Ajouter son spatial pour une source omnidirectionnel</span><span class="sxs-lookup"><span data-stu-id="c30af-127">Add spatial sound for an omnidirectional source</span></span>

<span data-ttu-id="c30af-128">Certains hologrammes dans son environnement de l’utilisateur émettent son équitablement dans toutes les directions.</span><span class="sxs-lookup"><span data-stu-id="c30af-128">Some holograms in the user's surroundings emit sound equally in all directions.</span></span> <span data-ttu-id="c30af-129">Le code suivant montre comment initialiser un APO pour émettre des sons omnidirectionnels.</span><span class="sxs-lookup"><span data-stu-id="c30af-129">The following code shows how to initialize an APO to emit omnidirectional sound.</span></span> <span data-ttu-id="c30af-130">Dans cet exemple, nous appliquons ce concept dans le cube en rotation à partir du modèle d’application Windows HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="c30af-130">In this example, we apply this concept to the spinning cube from the Windows Holographic app template.</span></span> <span data-ttu-id="c30af-131">Pour l’intégralité du code, consultez [OmnidirectionalSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/OmnidirectionalSound.cpp).</span><span class="sxs-lookup"><span data-stu-id="c30af-131">For the complete code listing, see [OmnidirectionalSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/OmnidirectionalSound.cpp).</span></span>

<span data-ttu-id="c30af-132">**Moteur audio spatial de la fenêtre prend uniquement en charge 48 samplerate k pour la lecture. La plupart des programmes d’intergiciel (middleware), comme Unity, convertit automatiquement les fichiers audio dans le format souhaité, mais si vous démarrez remanier à des niveaux inférieurs dans le système audio ou d’effectuer votre propre, ceci est très important à retenir empêcher les blocages ou des comportements indésirables tels que Défaillance du système HRTF.**</span><span class="sxs-lookup"><span data-stu-id="c30af-132">**Window's spatial sound engine only supports 48k samplerate for playback. Most middleware programs, like Unity, will automatically convert sound files into the desired format, but if you start tinkering at lower levels in the audio system or making your own, this is very important to remember to prevent crashes or undesired behaviour like HRTF system failure.**</span></span>

<span data-ttu-id="c30af-133">Tout d’abord, nous devons initialiser le APO.</span><span class="sxs-lookup"><span data-stu-id="c30af-133">First, we need to initialize the APO.</span></span> <span data-ttu-id="c30af-134">Dans notre application exemple HOLOGRAPHIQUE, nous choisissons pour ce faire, une fois que nous avons le **HolographicSpace**.</span><span class="sxs-lookup"><span data-stu-id="c30af-134">In our holographic sample app, we choose to do this once we have the **HolographicSpace**.</span></span>

<span data-ttu-id="c30af-135">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span><span class="sxs-lookup"><span data-stu-id="c30af-135">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span></span>

```
// Spatial sound
auto hr = m_omnidirectionalSound.Initialize(L"assets//MonoSound.wav");
```

<span data-ttu-id="c30af-136">L’implémentation de l’initialisation, à partir de *OmnidirectionalSound.cpp*:</span><span class="sxs-lookup"><span data-stu-id="c30af-136">The implementation of Initialize, from *OmnidirectionalSound.cpp*:</span></span>

```
// Initializes an APO that emits sound equally in all directions.
HRESULT OmnidirectionalSound::Initialize( LPCWSTR filename )
{
    // _audioFile is of type AudioFileReader, which is defined in AudioFileReader.cpp.
    auto hr = _audioFile.Initialize( filename );

    ComPtr<IXAPO> xapo;
    if ( SUCCEEDED( hr ) )
    {
        // Passing in nullptr as the first arg for HrtfApoInit initializes the APO with defaults of
        // omnidirectional sound with natural distance decay behavior.
        // CreateHrtfApo fails with E_NOTIMPL on unsupported platforms.
        hr = CreateHrtfApo( nullptr, &xapo );
    }

    if ( SUCCEEDED( hr ) )
    {
        // _hrtfParams is of type ComPtr<IXAPOHrtfParameters>.
        hr = xapo.As( &_hrtfParams );
    }

    // Set the default environment.
    if ( SUCCEEDED( hr ) )
    {
        hr = _hrtfParams->SetEnvironment( HrtfEnvironment::Outdoors );
    }

    // Initialize an XAudio2 graph that hosts the HRTF xAPO.
    // The source voice is used to submit audio data and control playback.
    if ( SUCCEEDED( hr ) )
    {
        hr = SetupXAudio2( _audioFile.GetFormat(), xapo.Get(), &_xaudio2, &_sourceVoice );
    }

    // Submit audio data to the source voice.
    if ( SUCCEEDED( hr ) )
    {
        XAUDIO2_BUFFER buffer{ };
        buffer.AudioBytes = static_cast<UINT32>( _audioFile.GetSize() );
        buffer.pAudioData = _audioFile.GetData();
        buffer.LoopCount = XAUDIO2_LOOP_INFINITE;

        // _sourceVoice is of type IXAudio2SourceVoice*.
        hr = _sourceVoice->SubmitSourceBuffer( &buffer );
    }

    return hr;
}
```

<span data-ttu-id="c30af-137">Après avoir configuré le APO pour HRTF, vous appelez [Démarrer](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire le fichier audio.</span><span class="sxs-lookup"><span data-stu-id="c30af-137">After the APO is configured for HRTF, you call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) on the source voice to play the audio.</span></span> <span data-ttu-id="c30af-138">Dans notre exemple d’application, nous choisissons placer dans une boucle afin que vous pouvez continuer à écouter le son provenant du cube.</span><span class="sxs-lookup"><span data-stu-id="c30af-138">In our sample app, we choose to put it on a loop so that you can continue to hear the sound coming from the cube.</span></span>

<span data-ttu-id="c30af-139">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span><span class="sxs-lookup"><span data-stu-id="c30af-139">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span></span>

```
if (SUCCEEDED(hr))
{
    m_omnidirectionalSound.SetEnvironment(HrtfEnvironment::Small);
    m_omnidirectionalSound.OnUpdate(m_spinningCubeRenderer->GetPosition());
    m_omnidirectionalSound.Start();
}
```

<span data-ttu-id="c30af-140">À partir de *OmnidirectionalSound.cpp*:</span><span class="sxs-lookup"><span data-stu-id="c30af-140">From *OmnidirectionalSound.cpp*:</span></span>

```
HRESULT OmnidirectionalSound::Start()
{
    _lastTick = GetTickCount64();
    return _sourceVoice->Start();
}
```

<span data-ttu-id="c30af-141">Désormais, chaque fois que nous mettons à jour le frame, nous devons mettre à jour la position de l’hologramme par rapport à l’appareil lui-même.</span><span class="sxs-lookup"><span data-stu-id="c30af-141">Now, whenever we update the frame, we need to update the hologram's position relative to the device itself.</span></span> <span data-ttu-id="c30af-142">Il s’agit, car HRTF positions sont toujours exprimées par rapport à la tête de l’utilisateur, y compris la position de tête et l’orientation.</span><span class="sxs-lookup"><span data-stu-id="c30af-142">This is because HRTF positions are always expressed relative to the user's head, including the head position and orientation.</span></span>

<span data-ttu-id="c30af-143">Pour ce faire, dans un HolographicSpace, nous devons construire une matrice de transformation à partir de notre système de coordonnées SpatialStationaryFrameOfReference à un système de coordonnées est fixé à l’appareil lui-même.</span><span class="sxs-lookup"><span data-stu-id="c30af-143">To do this in a HolographicSpace, we need to construct a transform matrix from our SpatialStationaryFrameOfReference coordinate system to a coordinate system that is fixed to the device itself.</span></span>

<span data-ttu-id="c30af-144">From *HolographicHrtfAudioSampleMain::Update()*:</span><span class="sxs-lookup"><span data-stu-id="c30af-144">From *HolographicHrtfAudioSampleMain::Update()*:</span></span>

```
m_spinningCubeRenderer->Update(m_timer);

SpatialPointerPose^ currentPose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
if (currentPose != nullptr)
{
    // Use a coordinate system built from a pointer pose.
    SpatialPointerPose^ pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
    if (pose != nullptr)
    {
        float3 headPosition = pose->Head->Position;
        float3 headUp = pose->Head->UpDirection;
        float3 headDirection = pose->Head->ForwardDirection;

        // To construct a rotation matrix, we need three vectors that are mutually orthogonal.
        // The first vector is the gaze vector.
        float3 negativeZAxis = normalize(headDirection);

        // The second vector should end up pointing away from the horizontal plane of the device.
        // We first guess by using the head "up" direction.
        float3 positiveYAxisGuess = normalize(headUp);

        // The third vector completes the set by being orthogonal to the other two.
        float3 positiveXAxis = normalize(cross(negativeZAxis, positiveYAxisGuess));

        // Now, we can correct our "up" vector guess by redetermining orthogonality.
        float3 positiveYAxis = normalize(cross(negativeZAxis, positiveXAxis));

        // The rotation matrix is formed as a standard basis rotation.
        float4x4 rotationTransform =
            {
            positiveXAxis.x, positiveYAxis.x, negativeZAxis.x, 0.f,
            positiveXAxis.y, positiveYAxis.y, negativeZAxis.y, 0.f,
            positiveXAxis.z, positiveYAxis.z, negativeZAxis.z, 0.f,
            0.f, 0.f, 0.f, 1.f,
            };

        // The translate transform can be constructed using the Windows::Foundation::Numerics API.
        float4x4 translationTransform = make_float4x4_translation(-headPosition);

        // Now, we have a basis transform from our spatial coordinate system to a device-relative
        // coordinate system.
        float4x4 coordinateSystemTransform = translationTransform * rotationTransform;

        // Reinterpret the cube position in the device's coordinate system.
        float3 cubeRelativeToHead = transform(m_spinningCubeRenderer->GetPosition(), coordinateSystemTransform);

        // Note that at (0, 0, 0) exactly, the HRTF audio will simply pass through audio. We can use a minimal offset
        // to simulate a zero distance when the hologram position vector is exactly at the device origin in order to
        // allow HRTF to continue functioning in this edge case.
        float distanceFromHologramToHead = length(cubeRelativeToHead);
        static const float distanceMin = 0.00001f;
        if (distanceFromHologramToHead < distanceMin)
        {
            cubeRelativeToHead = float3(0.f, distanceMin, 0.f);
        }

        // Position the spatial sound source on the hologram.
        m_omnidirectionalSound.OnUpdate(cubeRelativeToHead);

        // For debugging, it can be interesting to observe the distance in the debugger.
        /*
        std::wstring distanceString = L"Distance from hologram to head: ";
        distanceString += std::to_wstring(distanceFromHologramToHead);
        distanceString += L"\n";
        OutputDebugStringW(distanceString.c_str());
        */
    }
}
```

<span data-ttu-id="c30af-145">La position HRTF est appliquée directement à l’audio APO par la classe d’assistance OmnidirectionalSound.</span><span class="sxs-lookup"><span data-stu-id="c30af-145">The HRTF position is applied directly to the sound APO by the OmnidirectionalSound helper class.</span></span>

<span data-ttu-id="c30af-146">À partir de *OmnidirectionalSound::OnUpdate*:</span><span class="sxs-lookup"><span data-stu-id="c30af-146">From *OmnidirectionalSound::OnUpdate*:</span></span>

```
HRESULT OmnidirectionalSound::OnUpdate(_In_ Numerics::float3 position)
{
    auto hrtfPosition = HrtfPosition{ position.x, position.y, position.z };
    return _hrtfParams->SetSourcePosition(&hrtfPosition);
}
```

<span data-ttu-id="c30af-147">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="c30af-147">That's it!</span></span> <span data-ttu-id="c30af-148">Poursuivez votre lecture pour en savoir plus sur ce que vous pouvez faire avec audio HRTF et Windows HOLOGRAPHIQUE.</span><span class="sxs-lookup"><span data-stu-id="c30af-148">Continue reading to learn more about what you can do with HRTF audio and Windows Holographic.</span></span>

### <a name="initialize-spatial-sound-for-a-directional-source"></a><span data-ttu-id="c30af-149">Initialiser son spatial pour une source directionnel</span><span class="sxs-lookup"><span data-stu-id="c30af-149">Initialize spatial sound for a directional source</span></span>

<span data-ttu-id="c30af-150">Certains hologrammes dans son environnement de l’utilisateur émettent son principalement dans une seule direction.</span><span class="sxs-lookup"><span data-stu-id="c30af-150">Some holograms in the user's surroundings emit sound mostly in one direction.</span></span> <span data-ttu-id="c30af-151">Ce modèle sonore est nommé *cardioïde* parce qu’il ressemble à un cœur de dessin animé.</span><span class="sxs-lookup"><span data-stu-id="c30af-151">This sound pattern is named *cardioid* because it looks like a cartoon heart.</span></span> <span data-ttu-id="c30af-152">Le code suivant montre comment initialiser un APO pour émettre directionnelles audio.</span><span class="sxs-lookup"><span data-stu-id="c30af-152">The following code shows how to initialize an APO to emit directional sound.</span></span> <span data-ttu-id="c30af-153">Pour l’intégralité du code, consultez [CardioidSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CardioidSound.cpp) .</span><span class="sxs-lookup"><span data-stu-id="c30af-153">For the complete code listing, see [CardioidSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CardioidSound.cpp) .</span></span>

<span data-ttu-id="c30af-154">Après avoir configuré le APO pour HRTF, appelez [Démarrer](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire le fichier audio.</span><span class="sxs-lookup"><span data-stu-id="c30af-154">After the APO is configured for HRTF, call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) on the source voice to play the audio.</span></span>

```
// Initializes an APO that emits directional sound.
HRESULT CardioidSound::Initialize( LPCWSTR filename )
{
    // _audioFile is of type AudioFileReader, which is defined in AudioFileReader.cpp.
    auto hr = _audioFile.Initialize( filename );
    if ( SUCCEEDED( hr ) )
    {
        // Initialize with "Scaling" fully directional and "Order" with broad radiation pattern.
        // As the order goes higher, the cardioid directivity region becomes narrower.
        // Any direct path signal outside of the directivity region will be attenuated based on the scaling factor.
        // For example, if scaling is set to 1 (fully directional) the direct path signal outside of the directivity
        // region will be fully attenuated and only the reflections from the environment will be audible.
        hr = ConfigureApo( 1.0f, 4.0f );
    }
    return hr;
}

HRESULT CardioidSound::ConfigureApo( float scaling, float order )
{
    // Cardioid directivity configuration:
    // Directivity is specified at xAPO instance initialization and can't be changed per frame.
    // To change directivity, stop audio processing and reinitialize another APO instance with the new directivity.
    HrtfDirectivityCardioid cardioid;
    cardioid.directivity.type = HrtfDirectivityType::Cardioid;
    cardioid.directivity.scaling = scaling;
    cardioid.order = order;

    // APO intialization
    HrtfApoInit apoInit;
    apoInit.directivity = &cardioid.directivity;
    apoInit.distanceDecay = nullptr; // nullptr specifies natural distance decay behavior (simulates real world)

    // CreateHrtfApo fails with E_NOTIMPL on unsupported platforms.
    ComPtr<IXAPO> xapo;
    auto hr = CreateHrtfApo( &apoInit, &xapo );

    if ( SUCCEEDED( hr ) )
    {
        hr = xapo.As( &_hrtfParams );
    }

    // Set the initial environment.
    // Environment settings configure the "distance cues" used to compute the early and late reverberations.
    if ( SUCCEEDED( hr ) )
    {
        hr = _hrtfParams->SetEnvironment( _HrtfEnvironment::Outdoors );
    }

    // Initialize an XAudio2 graph that hosts the HRTF xAPO.
    // The source voice is used to submit audio data and control playback.
    if ( SUCCEEDED( hr ) )
    {
        hr = SetupXAudio2( _audioFile.GetFormat(), xapo.Get(), &_xaudio2, &_sourceVoice );
    }

    // Submit audio data to the source voice
    if ( SUCCEEDED( hr ) )
    {
        XAUDIO2_BUFFER buffer{ };
        buffer.AudioBytes = static_cast<UINT32>( _audioFile.GetSize() );
        buffer.pAudioData = _audioFile.GetData();
        buffer.LoopCount = XAUDIO2_LOOP_INFINITE;
        hr = _sourceVoice->SubmitSourceBuffer( &buffer );
    }

    return hr;
}
```

### <a name="implement-custom-decay"></a><span data-ttu-id="c30af-155">Implémenter une atténuation personnalisée</span><span class="sxs-lookup"><span data-stu-id="c30af-155">Implement custom decay</span></span>

<span data-ttu-id="c30af-156">Vous pouvez remplacer la fréquence à laquelle un son spatial tombe à distance et/ou à quelle distance elle coupe complètement.</span><span class="sxs-lookup"><span data-stu-id="c30af-156">You can override the rate at which a spatial sound falls off with distance and/or at what distance it cuts off completely.</span></span> <span data-ttu-id="c30af-157">Pour implémenter le comportement de DÉSINTÉGRATION personnalisé sur un son spatial, remplir un [HrtfDistanceDecay struct](https://msdn.microsoft.com/library/windows/desktop/mt186602.aspx) et assignez-la à la **distanceDecay** champ dans un [HrtfApoInit struct](https://msdn.microsoft.com/library/windows/desktop/mt186597.aspx) avant de le transmettre à la [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) (fonction).</span><span class="sxs-lookup"><span data-stu-id="c30af-157">To implement custom decay behavior on a spatial sound, populate an [HrtfDistanceDecay struct](https://msdn.microsoft.com/library/windows/desktop/mt186602.aspx) and assign it to the **distanceDecay** field in an [HrtfApoInit struct](https://msdn.microsoft.com/library/windows/desktop/mt186597.aspx) before passing it to the [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) function.</span></span>

<span data-ttu-id="c30af-158">Ajoutez le code suivant à la **initialiser** méthode indiqué précédemment pour spécifier le comportement de DÉSINTÉGRATION personnalisé.</span><span class="sxs-lookup"><span data-stu-id="c30af-158">Add the following code to the **Initialize** method shown previously to specify custom decay behavior.</span></span> <span data-ttu-id="c30af-159">Pour l’intégralité du code, consultez [CustomDecay.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CustomDecay.cpp).</span><span class="sxs-lookup"><span data-stu-id="c30af-159">For the complete code listing, see [CustomDecay.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CustomDecay.cpp).</span></span>

```
HRESULT CustomDecaySound::Initialize( LPCWSTR filename )
{
    auto hr = _audioFile.Initialize( filename );

    ComPtr<IXAPO> xapo;
    if ( SUCCEEDED( hr ) )
    {
        HrtfDistanceDecay customDecay;
        customDecay.type = HrtfDistanceDecayType::CustomDecay;               // Custom decay behavior, we'll pass in the gain value on every frame.
        customDecay.maxGain = 0;                                             // 0dB max gain
        customDecay.minGain = -96.0f;                                        // -96dB min gain
        customDecay.unityGainDistance = HRTF_DEFAULT_UNITY_GAIN_DISTANCE;    // Default unity gain distance
        customDecay.cutoffDistance = HRTF_DEFAULT_CUTOFF_DISTANCE;           // Default cutoff distance

        // Setting the directivity to nullptr specifies omnidirectional sound.
        HrtfApoInit init;
        init.directivity = nullptr;
        init.distanceDecay = &customDecay;

        // CreateHrtfApo will fail with E_NOTIMPL on unsupported platforms.
        hr = CreateHrtfApo( &init, &xapo );
    }
...
}
```
