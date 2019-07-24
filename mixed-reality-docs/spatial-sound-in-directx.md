---
title: Son spatial dans DirectX
description: Ajoutez du son spatial à vos applications Windows Mixed Reality basées sur DirectX à l’aide des bibliothèques audio XAudio2 et xAPO.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, son spatial, Apps, XAudio2, bas niveau, xAPO, bibliothèque audio, procédure pas à pas, DirectX
ms.openlocfilehash: 04d8c43ab400eed4cec5cbd848af5b888cb66e4b
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63550430"
---
# <a name="spatial-sound-in-directx"></a><span data-ttu-id="a882a-104">Son spatial dans DirectX</span><span class="sxs-lookup"><span data-stu-id="a882a-104">Spatial sound in DirectX</span></span>

<span data-ttu-id="a882a-105">Ajoutez du son spatial à vos applications Windows Mixed Reality basées sur DirectX à l’aide des bibliothèques audio [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049.aspx) et [xAPO](https://msdn.microsoft.com/library/windows/desktop/ee415735.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a882a-105">Add spatial sound to your Windows Mixed Reality apps based on DirectX by using the [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049.aspx) and [xAPO](https://msdn.microsoft.com/library/windows/desktop/ee415735.aspx) audio libraries.</span></span>

<span data-ttu-id="a882a-106">Cette rubrique utilise l’exemple de code de HolographicHRTFAudioSample.</span><span class="sxs-lookup"><span data-stu-id="a882a-106">This topic uses sample code from the HolographicHRTFAudioSample.</span></span>

>[!NOTE]
><span data-ttu-id="a882a-107">Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="a882a-107">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="a882a-108">Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="a882a-108">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="overview-of-head-relative-spatial-sound"></a><span data-ttu-id="a882a-109">Vue d’ensemble du son spatial spatial</span><span class="sxs-lookup"><span data-stu-id="a882a-109">Overview of Head Relative Spatial Sound</span></span>

<span data-ttu-id="a882a-110">Le son spatial est implémenté en tant qu' **objet de traitement audio (APO)** qui utilise un filtre de fonction de transfert de l' **en-tête (HRTF)** pour *spatialer* un flux audio ordinaire.</span><span class="sxs-lookup"><span data-stu-id="a882a-110">Spatial sound is implemented as an **audio processing object (APO)** that uses a **head related transfer function (HRTF)** filter to *spatialize* an ordinary audio stream.</span></span>

<span data-ttu-id="a882a-111">Incluez ces fichiers d’en-tête dans pch. h pour accéder aux API audio:</span><span class="sxs-lookup"><span data-stu-id="a882a-111">Include these header files in pch.h to access the audio APIs:</span></span>
* <span data-ttu-id="a882a-112">XAudio2. h</span><span class="sxs-lookup"><span data-stu-id="a882a-112">XAudio2.h</span></span>
* <span data-ttu-id="a882a-113">xapo. h</span><span class="sxs-lookup"><span data-stu-id="a882a-113">xapo.h</span></span>
* <span data-ttu-id="a882a-114">hrtfapoapi. h</span><span class="sxs-lookup"><span data-stu-id="a882a-114">hrtfapoapi.h</span></span>

<span data-ttu-id="a882a-115">Pour configurer un son spatial:</span><span class="sxs-lookup"><span data-stu-id="a882a-115">To set up spatial sound:</span></span>
1. <span data-ttu-id="a882a-116">Appelez [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) pour initialiser un nouveau APO pour l’audio HRTF.</span><span class="sxs-lookup"><span data-stu-id="a882a-116">Call [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) to initialize a new APO for HRTF audio.</span></span>
2. <span data-ttu-id="a882a-117">Affectez les [paramètres HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186608.aspx) et l' [environnement HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186604.aspx) pour définir les caractéristiques acoustiques du APO de son spatial.</span><span class="sxs-lookup"><span data-stu-id="a882a-117">Assign the [HRTF parameters](https://msdn.microsoft.com/library/windows/desktop/mt186608.aspx) and [HRTF environment](https://msdn.microsoft.com/library/windows/desktop/mt186604.aspx) to define the acoustic characteristics of the spatial sound APO.</span></span>
3. <span data-ttu-id="a882a-118">Configurez le moteur XAudio2 pour le traitement HRTF.</span><span class="sxs-lookup"><span data-stu-id="a882a-118">Set up the XAudio2 engine for HRTF processing.</span></span>
4. <span data-ttu-id="a882a-119">Créez un objet [IXAudio2SourceVoice](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.aspx) et appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx).</span><span class="sxs-lookup"><span data-stu-id="a882a-119">Create an [IXAudio2SourceVoice](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.aspx) object and call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx).</span></span>

## <a name="implementing-hrtf-and-spatial-sound-in-your-directx-app"></a><span data-ttu-id="a882a-120">Implémentation de HRTF et de son spatial dans votre application DirectX</span><span class="sxs-lookup"><span data-stu-id="a882a-120">Implementing HRTF and spatial sound in your DirectX app</span></span>

<span data-ttu-id="a882a-121">Vous pouvez obtenir un grand nombre d’effets en configurant HRTF APO avec différents paramètres et environnements.</span><span class="sxs-lookup"><span data-stu-id="a882a-121">You can achieve a variety of effects by configuring the HRTF APO with different parameters and environments.</span></span> <span data-ttu-id="a882a-122">Utilisez le code suivant pour explorer les possibilités.</span><span class="sxs-lookup"><span data-stu-id="a882a-122">Use the following code to explore the possibilities.</span></span> <span data-ttu-id="a882a-123">Téléchargez l’exemple de code plateforme Windows universelle à partir de cet emplacement: [Exemple de son spatial](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpatialSound)</span><span class="sxs-lookup"><span data-stu-id="a882a-123">Download the Universal Windows Platform code sample from here: [Spatial sound sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpatialSound)</span></span>

<span data-ttu-id="a882a-124">Les types d’assistance sont disponibles dans ces fichiers:</span><span class="sxs-lookup"><span data-stu-id="a882a-124">Helper types are available in these files:</span></span>
* <span data-ttu-id="a882a-125">[AudioFileReader. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/AudioFileReader.cpp): Charge des fichiers audio à l’aide de Media Foundation et de l' [interface IMFSourceReader](https://msdn.microsoft.com/library/windows/desktop/dd374655.aspx).</span><span class="sxs-lookup"><span data-stu-id="a882a-125">[AudioFileReader.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/AudioFileReader.cpp): Loads audio files by using Media Foundation and the [IMFSourceReader interface](https://msdn.microsoft.com/library/windows/desktop/dd374655.aspx).</span></span>
* <span data-ttu-id="a882a-126">[XAudio2Helpers. h](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/XAudio2Helpers.h): Implémente la fonction **SetupXAudio2** pour initialiser XAudio2 pour le traitement HRTF.</span><span class="sxs-lookup"><span data-stu-id="a882a-126">[XAudio2Helpers.h](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/XAudio2Helpers.h): Implements the **SetupXAudio2** function to initialize XAudio2 for HRTF processing.</span></span>

### <a name="add-spatial-sound-for-an-omnidirectional-source"></a><span data-ttu-id="a882a-127">Ajouter un son spatial pour une source omnidirectionnelle</span><span class="sxs-lookup"><span data-stu-id="a882a-127">Add spatial sound for an omnidirectional source</span></span>

<span data-ttu-id="a882a-128">Certains hologrammes dans l’environnement de l’utilisateur émettent un son de la même manière dans toutes les directions.</span><span class="sxs-lookup"><span data-stu-id="a882a-128">Some holograms in the user's surroundings emit sound equally in all directions.</span></span> <span data-ttu-id="a882a-129">Le code suivant montre comment initialiser un APO pour émettre un son omnidirectionnel.</span><span class="sxs-lookup"><span data-stu-id="a882a-129">The following code shows how to initialize an APO to emit omnidirectional sound.</span></span> <span data-ttu-id="a882a-130">Dans cet exemple, nous appliquons ce concept au cube tournant à partir du modèle d’application Windows holographique.</span><span class="sxs-lookup"><span data-stu-id="a882a-130">In this example, we apply this concept to the spinning cube from the Windows Holographic app template.</span></span> <span data-ttu-id="a882a-131">Pour obtenir la liste complète du code, consultez [OmnidirectionalSound. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/OmnidirectionalSound.cpp).</span><span class="sxs-lookup"><span data-stu-id="a882a-131">For the complete code listing, see [OmnidirectionalSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/OmnidirectionalSound.cpp).</span></span>

<span data-ttu-id="a882a-132">**Le moteur du son spatial ne prend en charge que les samplerate 48K pour la lecture. La plupart des programmes middleware, comme Unity, convertissent automatiquement les fichiers audio au format souhaité, mais si vous commencez à utiliser des niveaux inférieurs dans le système audio ou à créer les vôtres, il est très important de se souvenir d’éviter les pannes ou le comportement indésirable comme Échec du système HRTF.**</span><span class="sxs-lookup"><span data-stu-id="a882a-132">**Window's spatial sound engine only supports 48k samplerate for playback. Most middleware programs, like Unity, will automatically convert sound files into the desired format, but if you start tinkering at lower levels in the audio system or making your own, this is very important to remember to prevent crashes or undesired behaviour like HRTF system failure.**</span></span>

<span data-ttu-id="a882a-133">Tout d’abord, nous devons initialiser le APO.</span><span class="sxs-lookup"><span data-stu-id="a882a-133">First, we need to initialize the APO.</span></span> <span data-ttu-id="a882a-134">Dans notre exemple d’application holographique, nous choisissons de le faire une fois que nous aurons **HolographicSpace**.</span><span class="sxs-lookup"><span data-stu-id="a882a-134">In our holographic sample app, we choose to do this once we have the **HolographicSpace**.</span></span>

<span data-ttu-id="a882a-135">À partir de *HolographicHrtfAudioSampleMain:: SetHolographicSpace ()* :</span><span class="sxs-lookup"><span data-stu-id="a882a-135">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span></span>

```
// Spatial sound
auto hr = m_omnidirectionalSound.Initialize(L"assets//MonoSound.wav");
```

<span data-ttu-id="a882a-136">Implémentation de Initialize, à partir de *OmnidirectionalSound. cpp*:</span><span class="sxs-lookup"><span data-stu-id="a882a-136">The implementation of Initialize, from *OmnidirectionalSound.cpp*:</span></span>

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

<span data-ttu-id="a882a-137">Une fois l’APO configuré pour HRTF, vous appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire l’audio.</span><span class="sxs-lookup"><span data-stu-id="a882a-137">After the APO is configured for HRTF, you call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) on the source voice to play the audio.</span></span> <span data-ttu-id="a882a-138">Dans notre exemple d’application, nous choisissons de le placer sur une boucle afin que vous puissiez continuer à entendre le son provenant du cube.</span><span class="sxs-lookup"><span data-stu-id="a882a-138">In our sample app, we choose to put it on a loop so that you can continue to hear the sound coming from the cube.</span></span>

<span data-ttu-id="a882a-139">À partir de *HolographicHrtfAudioSampleMain:: SetHolographicSpace ()* :</span><span class="sxs-lookup"><span data-stu-id="a882a-139">From *HolographicHrtfAudioSampleMain::SetHolographicSpace()*:</span></span>

```
if (SUCCEEDED(hr))
{
    m_omnidirectionalSound.SetEnvironment(HrtfEnvironment::Small);
    m_omnidirectionalSound.OnUpdate(m_spinningCubeRenderer->GetPosition());
    m_omnidirectionalSound.Start();
}
```

<span data-ttu-id="a882a-140">À partir de *OmnidirectionalSound. cpp*:</span><span class="sxs-lookup"><span data-stu-id="a882a-140">From *OmnidirectionalSound.cpp*:</span></span>

```
HRESULT OmnidirectionalSound::Start()
{
    _lastTick = GetTickCount64();
    return _sourceVoice->Start();
}
```

<span data-ttu-id="a882a-141">Maintenant, chaque fois que nous mettons à jour le cadre, nous devons mettre à jour la position de l’hologramme par rapport à l’appareil lui-même.</span><span class="sxs-lookup"><span data-stu-id="a882a-141">Now, whenever we update the frame, we need to update the hologram's position relative to the device itself.</span></span> <span data-ttu-id="a882a-142">Cela est dû au fait que les positions HRTF sont toujours exprimées par rapport au début de l’utilisateur, y compris la position et l’orientation de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="a882a-142">This is because HRTF positions are always expressed relative to the user's head, including the head position and orientation.</span></span>

<span data-ttu-id="a882a-143">Pour effectuer cette opération dans un HolographicSpace, nous devons construire une matrice de transformation à partir de notre système de coordonnées SpatialStationaryFrameOfReference sur un système de coordonnées qui est fixe à l’appareil lui-même.</span><span class="sxs-lookup"><span data-stu-id="a882a-143">To do this in a HolographicSpace, we need to construct a transform matrix from our SpatialStationaryFrameOfReference coordinate system to a coordinate system that is fixed to the device itself.</span></span>

<span data-ttu-id="a882a-144">À partir de *HolographicHrtfAudioSampleMain:: Update ()* :</span><span class="sxs-lookup"><span data-stu-id="a882a-144">From *HolographicHrtfAudioSampleMain::Update()*:</span></span>

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

<span data-ttu-id="a882a-145">La position HRTF est appliquée directement au son APO par la classe d’assistance OmnidirectionalSound.</span><span class="sxs-lookup"><span data-stu-id="a882a-145">The HRTF position is applied directly to the sound APO by the OmnidirectionalSound helper class.</span></span>

<span data-ttu-id="a882a-146">À partir de *OmnidirectionalSound:: OnUpdate*:</span><span class="sxs-lookup"><span data-stu-id="a882a-146">From *OmnidirectionalSound::OnUpdate*:</span></span>

```
HRESULT OmnidirectionalSound::OnUpdate(_In_ Numerics::float3 position)
{
    auto hrtfPosition = HrtfPosition{ position.x, position.y, position.z };
    return _hrtfParams->SetSourcePosition(&hrtfPosition);
}
```

<span data-ttu-id="a882a-147">C’est tout !</span><span class="sxs-lookup"><span data-stu-id="a882a-147">That's it!</span></span> <span data-ttu-id="a882a-148">Poursuivez la lecture pour en savoir plus sur ce que vous pouvez faire avec HRTF audio et Windows holographique.</span><span class="sxs-lookup"><span data-stu-id="a882a-148">Continue reading to learn more about what you can do with HRTF audio and Windows Holographic.</span></span>

### <a name="initialize-spatial-sound-for-a-directional-source"></a><span data-ttu-id="a882a-149">Initialiser le son spatial pour une source directionnelle</span><span class="sxs-lookup"><span data-stu-id="a882a-149">Initialize spatial sound for a directional source</span></span>

<span data-ttu-id="a882a-150">Certains hologrammes dans l’environnement de l’utilisateur émettent un son principalement dans une seule direction.</span><span class="sxs-lookup"><span data-stu-id="a882a-150">Some holograms in the user's surroundings emit sound mostly in one direction.</span></span> <span data-ttu-id="a882a-151">Ce modèle de son est appelé « *cardioïde* », car il ressemble à un coeur de dessin animé.</span><span class="sxs-lookup"><span data-stu-id="a882a-151">This sound pattern is named *cardioid* because it looks like a cartoon heart.</span></span> <span data-ttu-id="a882a-152">Le code suivant montre comment initialiser un APO pour émettre un son directionnel.</span><span class="sxs-lookup"><span data-stu-id="a882a-152">The following code shows how to initialize an APO to emit directional sound.</span></span> <span data-ttu-id="a882a-153">Pour obtenir la liste complète du code, consultez [CardioidSound. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CardioidSound.cpp) .</span><span class="sxs-lookup"><span data-stu-id="a882a-153">For the complete code listing, see [CardioidSound.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CardioidSound.cpp) .</span></span>

<span data-ttu-id="a882a-154">Une fois l’APO configuré pour HRTF, appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire l’audio.</span><span class="sxs-lookup"><span data-stu-id="a882a-154">After the APO is configured for HRTF, call [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) on the source voice to play the audio.</span></span>

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

### <a name="implement-custom-decay"></a><span data-ttu-id="a882a-155">Implémenter une atténuation personnalisée</span><span class="sxs-lookup"><span data-stu-id="a882a-155">Implement custom decay</span></span>

<span data-ttu-id="a882a-156">Vous pouvez remplacer la vitesse à laquelle un son spatial se situe à distance et/ou à la distance complètement coupée.</span><span class="sxs-lookup"><span data-stu-id="a882a-156">You can override the rate at which a spatial sound falls off with distance and/or at what distance it cuts off completely.</span></span> <span data-ttu-id="a882a-157">Pour implémenter un comportement de désintégration personnalisé sur un son spatial, remplissez un [struct HrtfDistanceDecay](https://msdn.microsoft.com/library/windows/desktop/mt186602.aspx) et affectez-le au champ **distanceDecay** dans un [struct HrtfApoInit](https://msdn.microsoft.com/library/windows/desktop/mt186597.aspx) avant de le passer à la fonction [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) .</span><span class="sxs-lookup"><span data-stu-id="a882a-157">To implement custom decay behavior on a spatial sound, populate an [HrtfDistanceDecay struct](https://msdn.microsoft.com/library/windows/desktop/mt186602.aspx) and assign it to the **distanceDecay** field in an [HrtfApoInit struct](https://msdn.microsoft.com/library/windows/desktop/mt186597.aspx) before passing it to the [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) function.</span></span>

<span data-ttu-id="a882a-158">Ajoutez le code suivant à la méthode **Initialize** indiquée précédemment pour spécifier un comportement de désintégration personnalisée.</span><span class="sxs-lookup"><span data-stu-id="a882a-158">Add the following code to the **Initialize** method shown previously to specify custom decay behavior.</span></span> <span data-ttu-id="a882a-159">Pour obtenir la liste complète du code, consultez [CustomDecay. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CustomDecay.cpp).</span><span class="sxs-lookup"><span data-stu-id="a882a-159">For the complete code listing, see [CustomDecay.cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CustomDecay.cpp).</span></span>

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
