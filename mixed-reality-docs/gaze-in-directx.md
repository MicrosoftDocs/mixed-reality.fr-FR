---
title: HEAD et surveillez les regards dans DirectX
description: Guide du développeur pour l’utilisation du pointage de regard principal et les yeux dans les applications DirectX natives.
author: caseymeekhof
ms.author: cmeekhof
ms.date: 05/09/2019
ms.topic: article
keywords: regards, regards principal, chef de suivi, suivi de le œil, directx, entrée, hologrammes
ms.openlocfilehash: ac72c5305527ed2d68945aeb32051cf2246a736e
ms.sourcegitcommit: 60060386305eabfac2758a2c861a43c36286b151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453742"
---
# <a name="head-and-eye-gaze-input-in-directx"></a>Principaux et surveiller les regards entrée dans DirectX

Dans Windows Mixed Reality, yeux et regards principal entrée est utilisée pour déterminer ce que l’utilisateur consulte. Cela peut être utilisé pour les modèles d’entrée principaux tels que le lecteur [head regards et validation](gaze-and-commit.md)et également pour fournir un contexte pour les types d’interactions. Il existe deux types de regards vecteurs disponibles via l’API : head regards et regards de œil.  Les deux sont fournis sous forme de trois dimensions ray avec une origine et la direction. Les applications peuvent ensuite raycast dans leur arrière-plan ou le monde réel et déterminer ce que l’utilisateur cible.

**Utilisation de la tête** représente la direction dans laquelle la tête de l’utilisateur est référencée dans. Pensez-y comme à la position et la direction avant de l’appareil lui-même, avec la position qui représente le centre de point entre les deux affichages.  Head regards est disponible sur tous les appareils de réalité mixte.

**Les regards yeux** représente la direction dans laquelle vous cherchent à yeux de l’utilisateur. L’origine se trouve entre les yeux de l’utilisateur.  Il est disponible sur les appareils de réalité mixte qui incluent un système de suivi de le œil.

Head et surveillez les rayons du pointage de regard sont accessibles via le [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API. Il vous suffit d’appeler [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose à l’horodatage spécifié et [système de coordonnées](coordinate-systems-in-directx.md). Ce SpatialPointerPose contient un principal du pointage de regard origine et la direction. Il contient également une origine des regards yeux et la direction si le suivi de le œil est disponible.

## <a name="using-head-gaze"></a>À l’aide des regards principal

Pour accéder à la tête du pointage de regard, démarrez en appelant [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) pour recevoir un nouvel objet SpatialPointerPose. Vous devez transmettre les paramètres suivants.
 - Un [SpatialCoordinateSystem](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialcoordinatesystem) qui représente le système de coordonnées de votre choix pour les regards principal. Ceci est représenté par le *coordinateSystem* variable dans le code suivant. Pour plus d’informations, visitez notre [systèmes de coordonnées](coordinate-systems-in-directx.md) guide du développeur.
 - Un [Timestamp](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframeprediction.timestamp#Windows_Graphics_Holographic_HolographicFramePrediction_Timestamp) qui représente l’heure exacte de la pose principale demandée.  En règle générale, vous allez utiliser un horodatage qui correspond à la fois lorsque le frame actuel s’affiche. Vous pouvez obtenir cet horodatage affichage prévues à partir d’un [HolographicFramePrediction](https://docs.microsoft.com/en-us/uwp/api/Windows.Graphics.Holographic.HolographicFramePrediction) objet, qui est accessible via actuel [HolographicFrame](https://docs.microsoft.com/en-us/uwp/api/windows.graphics.holographic.holographicframe).  Cet objet HolographicFramePrediction est représenté par le *prédiction* variable dans le code suivant.

 Une fois que vous avez un SpatialPointerPose valide, la position de tête et vers l’avant sont accessibles en tant que propriétés.  Le code suivant montre comment y accéder.

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

## <a name="using-eye-gaze"></a>À l’aide du pointage de regard œil

L’API de regards yeux est très similaire à regards principal.  Il utilise le même [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) API, qui fournit un rayon origine et la direction que vous pouvez raycast par rapport à votre scène.  La seule différence est que vous devez explicitement activer le suivi des yeux avant de l’utiliser. Pour ce faire, vous devez effectuer deux étapes :
1. Demander l’autorisation d’utilisateur à utiliser les yeux dans votre application.
2. Activer la fonctionnalité « Entrée utilisation » dans votre manifeste du package.

### <a name="requesting-access-to-gaze-input"></a>Demande d’accès à l’utilisation d’entrée
Lors du démarrage de votre application, appelez [EyesPose::RequestAccessAsync](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.requestaccessasync#Windows_Perception_People_EyesPose_RequestAccessAsync) pour demander l’accès pour le suivi des yeux. Le système demande à l’utilisateur si nécessaire et retourner [GazeInputAccessStatus::Allowed](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.gazeinputaccessstatus) une fois que l’accès a été accordé. Il s’agit d’un appel asynchrone, elle nécessite un peu de gestion supplémentaire. L’exemple suivant démarre un std::thread détachée à attendre le résultat, qui est stockée à une variable de membre appelée *m_isEyeTrackingEnabled*.

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
À partir d’un thread détaché est qu’une seule option pour la gestion des appels asynchrones.  Vous pouvez également utiliser la nouvelle [co_await](https://docs.microsoft.com/en-us/windows/uwp/cpp-and-winrt-apis/concurrency) fonctionnalités prises en charge par C++/WinRT.
Voici un autre exemple de demande d’autorisation utilisateur :
-   EyesPose::IsSupported() permet à l’application déclencher la boîte de dialogue d’autorisation uniquement s’il existe un suivi de l’oeil.
-   GazeInputAccessStatus m_gazeInputAccessStatus ; Cela vise à éviter surgit à l’invite d’autorisation indéfiniment.

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


### <a name="declaring-the-gaze-input-capability"></a>Déclarer la *entrée regards* fonctionnalité

Double-cliquez sur le fichier appxmanifest dans *l’Explorateur de solutions*.  Puis accédez à la *fonctionnalités* section et vérifier le *entrée regards* fonctionnalité. 

![Capacité d’entrée du pointage de regard](images/gaze-input-capability.png)

Cette opération ajoute les lignes suivantes à la *Package* section dans le fichier appxmanifest :
```xml
  <Capabilities>
    <DeviceCapability Name="gazeInput" />
  </Capabilities>
```

### <a name="getting-the-eye-gaze-ray"></a>Obtenir le rayon de regards œil
Une fois que vous avez reçu l’accès à ET, vous êtes libre saisir le rayon de regards yeux chaque trame.  Comme avec les regards principal, obtenir le [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/Windows.UI.Input.Spatial.SpatialPointerPose) en appelant [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) avec un horodatage souhaité et d’un système de coordonnées. Contient le SpatialPointerPose un [EyesPose](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose) via la [yeux](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.eyes) propriété. Cela n’est pas null uniquement si le suivi de le œil est activé. À partir de là, vous pouvez vérifier si l’utilisateur dans l’appareil a un œil d’étalonnage de suivi en appelant [EyesPose::IsCalibrationValid](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.iscalibrationvalid#Windows_Perception_People_EyesPose_IsCalibrationValid).  Ensuite, utilisez le [les regards](https://docs.microsoft.com/en-us/uwp/api/windows.perception.people.eyespose.gaze#Windows_Perception_People_EyesPose_Gaze) propriété à obtenir l’un [SpatialRay](https://docs.microsoft.com/en-us/uwp/api/windows.perception.spatial.spatialray) réceptrice le œil les regards position et la direction. La propriété regards peut parfois être null, veillez à vérifier cela. Cela peut est se produire si un utilisateur étalonné ferme temporairement leurs yeux.

Le code suivant montre comment accéder au rayon de regards yeux.

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

## <a name="correlating-gaze-with-other-inputs"></a>Corrélation des regards avec les autres entrées

Parfois, vous constaterez que vous avez besoin une [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) qui correspond à un événement dans le passé. Par exemple, si l’utilisateur effectue un Air appuyez sur, votre application souhaiterez peut-être savoir qu’ils ont été consultant. Pour cela, il vous suffit à l’aide de [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp) la trame prédite temps seraient inexacte en raison de la latence entre le traitement du système d’entrée et d’affichage de l’heure. En outre, si vous utilisez des regards d’oeil pour le ciblage, nos yeux ont tendance à déplacer même avant la fin d’une action de validation. Cela est moins de problèmes pour un Tap Air simple, mais devient plus importante lors de la combinaison la durée pendant laquelle les commandes vocales avec des mouvements d’oeil rapide. Une pour gérer ce scénario consiste à effectuer un appel supplémentaire à [SpatialPointerPose::TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose.trygetattimestamp), à l’aide d’une date et heure historiques qui correspond à l’événement d’entrée.  

Toutefois, pour l’entrée qui traverse le SpatialInteractionManager, il existe une méthode plus facile. Le [SpatialInteractionSourceState](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate) a son propre [TryGetAtTimestamp](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialinteractionsourcestate.trygetpointerpose) (fonction). Appel qui fournira un parfaitement corrélés [SpatialPointerPose](https://docs.microsoft.com/en-us/uwp/api/windows.ui.input.spatial.spatialpointerpose) sans devinette. Pour plus d’informations sur l’utilisation des SpatialInteractionSourceStates, examinons le [mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md) documentation.

## <a name="see-also"></a>Voir aussi
* [Modèle d’entrée principal du pointage de regard et validation](gaze-and-commit.md)
* [Yeux sur HoloLens 2](eye-tracking.md)
* [Systèmes de coordonnées dans DirectX](coordinate-systems-in-directx.md)
* [Entrée vocale dans DirectX](voice-input-in-directx.md)
* [Mains et contrôleurs de mouvement dans DirectX](hands-and-motion-controllers-in-directx.md)
