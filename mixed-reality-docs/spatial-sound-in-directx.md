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
# <a name="spatial-sound-in-directx"></a>Son spatial dans DirectX

Ajoutez du son spatial à vos applications Windows Mixed Reality basées sur DirectX à l’aide des bibliothèques audio [XAudio2](https://msdn.microsoft.com/library/windows/desktop/hh405049.aspx) et [xAPO](https://msdn.microsoft.com/library/windows/desktop/ee415735.aspx) .

Cette rubrique utilise l’exemple de code de HolographicHRTFAudioSample.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="overview-of-head-relative-spatial-sound"></a>Vue d’ensemble du son spatial spatial

Le son spatial est implémenté en tant qu' **objet de traitement audio (APO)** qui utilise un filtre de fonction de transfert de l' **en-tête (HRTF)** pour *spatialer* un flux audio ordinaire.

Incluez ces fichiers d’en-tête dans pch. h pour accéder aux API audio:
* XAudio2. h
* xapo. h
* hrtfapoapi. h

Pour configurer un son spatial:
1. Appelez [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) pour initialiser un nouveau APO pour l’audio HRTF.
2. Affectez les [paramètres HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186608.aspx) et l' [environnement HRTF](https://msdn.microsoft.com/library/windows/desktop/mt186604.aspx) pour définir les caractéristiques acoustiques du APO de son spatial.
3. Configurez le moteur XAudio2 pour le traitement HRTF.
4. Créez un objet [IXAudio2SourceVoice](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.aspx) et appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx).

## <a name="implementing-hrtf-and-spatial-sound-in-your-directx-app"></a>Implémentation de HRTF et de son spatial dans votre application DirectX

Vous pouvez obtenir un grand nombre d’effets en configurant HRTF APO avec différents paramètres et environnements. Utilisez le code suivant pour explorer les possibilités. Téléchargez l’exemple de code plateforme Windows universelle à partir de cet emplacement: [Exemple de son spatial](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/SpatialSound)

Les types d’assistance sont disponibles dans ces fichiers:
* [AudioFileReader. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/AudioFileReader.cpp): Charge des fichiers audio à l’aide de Media Foundation et de l' [interface IMFSourceReader](https://msdn.microsoft.com/library/windows/desktop/dd374655.aspx).
* [XAudio2Helpers. h](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/XAudio2Helpers.h): Implémente la fonction **SetupXAudio2** pour initialiser XAudio2 pour le traitement HRTF.

### <a name="add-spatial-sound-for-an-omnidirectional-source"></a>Ajouter un son spatial pour une source omnidirectionnelle

Certains hologrammes dans l’environnement de l’utilisateur émettent un son de la même manière dans toutes les directions. Le code suivant montre comment initialiser un APO pour émettre un son omnidirectionnel. Dans cet exemple, nous appliquons ce concept au cube tournant à partir du modèle d’application Windows holographique. Pour obtenir la liste complète du code, consultez [OmnidirectionalSound. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/OmnidirectionalSound.cpp).

**Le moteur du son spatial ne prend en charge que les samplerate 48K pour la lecture. La plupart des programmes middleware, comme Unity, convertissent automatiquement les fichiers audio au format souhaité, mais si vous commencez à utiliser des niveaux inférieurs dans le système audio ou à créer les vôtres, il est très important de se souvenir d’éviter les pannes ou le comportement indésirable comme Échec du système HRTF.**

Tout d’abord, nous devons initialiser le APO. Dans notre exemple d’application holographique, nous choisissons de le faire une fois que nous aurons **HolographicSpace**.

À partir de *HolographicHrtfAudioSampleMain:: SetHolographicSpace ()* :

```
// Spatial sound
auto hr = m_omnidirectionalSound.Initialize(L"assets//MonoSound.wav");
```

Implémentation de Initialize, à partir de *OmnidirectionalSound. cpp*:

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

Une fois l’APO configuré pour HRTF, vous appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire l’audio. Dans notre exemple d’application, nous choisissons de le placer sur une boucle afin que vous puissiez continuer à entendre le son provenant du cube.

À partir de *HolographicHrtfAudioSampleMain:: SetHolographicSpace ()* :

```
if (SUCCEEDED(hr))
{
    m_omnidirectionalSound.SetEnvironment(HrtfEnvironment::Small);
    m_omnidirectionalSound.OnUpdate(m_spinningCubeRenderer->GetPosition());
    m_omnidirectionalSound.Start();
}
```

À partir de *OmnidirectionalSound. cpp*:

```
HRESULT OmnidirectionalSound::Start()
{
    _lastTick = GetTickCount64();
    return _sourceVoice->Start();
}
```

Maintenant, chaque fois que nous mettons à jour le cadre, nous devons mettre à jour la position de l’hologramme par rapport à l’appareil lui-même. Cela est dû au fait que les positions HRTF sont toujours exprimées par rapport au début de l’utilisateur, y compris la position et l’orientation de l’en-tête.

Pour effectuer cette opération dans un HolographicSpace, nous devons construire une matrice de transformation à partir de notre système de coordonnées SpatialStationaryFrameOfReference sur un système de coordonnées qui est fixe à l’appareil lui-même.

À partir de *HolographicHrtfAudioSampleMain:: Update ()* :

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

La position HRTF est appliquée directement au son APO par la classe d’assistance OmnidirectionalSound.

À partir de *OmnidirectionalSound:: OnUpdate*:

```
HRESULT OmnidirectionalSound::OnUpdate(_In_ Numerics::float3 position)
{
    auto hrtfPosition = HrtfPosition{ position.x, position.y, position.z };
    return _hrtfParams->SetSourcePosition(&hrtfPosition);
}
```

C’est tout ! Poursuivez la lecture pour en savoir plus sur ce que vous pouvez faire avec HRTF audio et Windows holographique.

### <a name="initialize-spatial-sound-for-a-directional-source"></a>Initialiser le son spatial pour une source directionnelle

Certains hologrammes dans l’environnement de l’utilisateur émettent un son principalement dans une seule direction. Ce modèle de son est appelé « *cardioïde* », car il ressemble à un coeur de dessin animé. Le code suivant montre comment initialiser un APO pour émettre un son directionnel. Pour obtenir la liste complète du code, consultez [CardioidSound. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CardioidSound.cpp) .

Une fois l’APO configuré pour HRTF, appelez [Start](https://msdn.microsoft.com/library/windows/desktop/microsoft.directx_sdk.ixaudio2sourcevoice.ixaudio2sourcevoice.start.aspx) sur la voix source pour lire l’audio.

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

### <a name="implement-custom-decay"></a>Implémenter une atténuation personnalisée

Vous pouvez remplacer la vitesse à laquelle un son spatial se situe à distance et/ou à la distance complètement coupée. Pour implémenter un comportement de désintégration personnalisé sur un son spatial, remplissez un [struct HrtfDistanceDecay](https://msdn.microsoft.com/library/windows/desktop/mt186602.aspx) et affectez-le au champ **distanceDecay** dans un [struct HrtfApoInit](https://msdn.microsoft.com/library/windows/desktop/mt186597.aspx) avant de le passer à la fonction [CreateHrtfApo](https://msdn.microsoft.com/library/windows/desktop/mt186596.aspx) .

Ajoutez le code suivant à la méthode **Initialize** indiquée précédemment pour spécifier un comportement de désintégration personnalisée. Pour obtenir la liste complète du code, consultez [CustomDecay. cpp](https://github.com/Microsoft/Windows-universal-samples/blob/master/Samples/SpatialSound/cpp/CustomDecay.cpp).

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
