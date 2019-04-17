---
title: Regards, les mouvements et les contrôleurs de mouvement dans DirectX
description: Combinaison d’entrée peuvent provenir du pointage de regard, les mouvements et les contrôleurs de mouvement, vous pouvez activer un utilisateur pour placer un hologramme dans votre application.
author: thetuvix
ms.author: alexturn
ms.date: 02/24/2019
ms.topic: article
keywords: regards, mouvements, contrôleurs de mouvement, directx, entrée, hologrammes
ms.openlocfilehash: 7cee3d3d7fbcd903eae0376e205034b9cc4ead3b
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597121"
---
# <a name="gaze-gestures-and-motion-controllers-in-directx"></a>Regards, les mouvements et les contrôleurs de mouvement dans DirectX

Si vous vous apprêtez à générer directement sur la plateforme, vous devrez gérer l’entrée provenant de l’utilisateur, tels que recherche où l’utilisateur [regards principal](gaze.md) et ce que l’utilisateur a sélectionné avec [mouvements](gestures.md) ou [contrôleurs de mouvement](motion-controllers.md). Combinaison de ces formes de saisie, vous pouvez activer un utilisateur pour placer un [hologramme](hologram.md) dans votre application. Le [modèle d’application HOLOGRAPHIQUE](creating-a-holographic-directx-project.md) a un exemple facile à utiliser.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="gaze-input"></a>Entrée avec le pointage du regard

Pour accéder à l’utilisateur [regards principal](gaze.md), vous utilisez le [SpatialPointerPose](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialpointerpose.aspx) type. Le modèle d’application HOLOGRAPHIQUE inclut le code de base pour les regards de présentation. Ce code fournit un vecteur qui pointe vers l’avant entre les yeux de l’utilisateur, compte tenu de position de l’appareil et l’orientation dans une donnée [système de coordonnées](coordinate-systems-in-directx.md).




```cpp
void SpinningCubeRenderer::PositionHologram(SpatialPointerPose^ pointerPose)
{
    if (pointerPose != nullptr)
    {
        // Get the gaze direction relative to the given coordinate system.
        const float3 headPosition    = pointerPose->Head->Position;
        const float3 headDirection   = pointerPose->Head->ForwardDirection;
    
        // The hologram is positioned two meters along the user's gaze direction.
        static const float distanceFromUser = 2.0f; // meters
        const float3 gazeAtTwoMeters        = headPosition + (distanceFromUser * headDirection);
    
        // This will be used as the translation component of the hologram's
        // model transform.
        SetPosition(gazeAtTwoMeters);
    }
}
```

Vous trouverez peut-être vous demandez : « Mais d'où provient le système de coordonnées ? »

Nous allons répondre à cette question. Dans de notre AppMain **mise à jour** (fonction), nous traité un événement d’entrée spatial en acquérant par rapport à système de coordonnées pour notre StationaryFrameOfReference. Rappelez-vous que le StationaryFrameOfReference a été créé lorsque nous configurons le [HolographicSpace](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx), et le système de coordonnées a été acquis au début de [mise à jour](rendering-in-directx.md).




```cpp
// Check for new input state since the last frame.
SpatialInteractionSourceState^ pointerState = m_spatialInputHandler->CheckForInput();
if (pointerState != nullptr)
{
    // When a Pressed gesture is detected, the sample hologram will be repositioned
    // two meters in front of the user.
    m_spinningCubeRenderer->PositionHologram(
        pointerState->TryGetPointerPose(currentCoordinateSystem)
        );
}
```

Notez que les données sont liées à un état de pointeur quelconque. Nous l’obtenir à partir d’un événement d’entrée spatial. L’objet de données d’événement inclut un système de coordonnées, afin que vous pouvez toujours associer la direction du regard au moment de l’événement à quelque système de coordonnées spatial vous avez besoin. En fait, vous devez le faire afin d’obtenir la pose de pointeur.

> [!NOTE]
> Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).

## <a name="gesture-and-motion-controller-input"></a>Contrôleur de mouvement et le mouvement d’entrée

En réalité mixte de Windows, les deux main [mouvements](gestures.md) et [contrôleurs de mouvement](motion-controllers.md) sont gérées via la même entrée spatiale API, trouvée dans le [Windows.UI.Input.Spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial) espace de noms. Cela vous permet de gérer facilement des actions courantes telles que **sélectionnez** appuie sur la même façon entre les mains et contrôleurs de mouvement.

Il existe deux niveaux d’API, vous pouvez cibler lors de la gestion des contrôleurs de mouvement ou de mouvements en réalité mixte :
* [Interactions](gestures.md#the-two-core-gestures-of-hololens) ([SourcePressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed.aspx), [SourceReleased](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased.aspx) et [SourceUpdated](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated.aspx)), accessible à l’aide un [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx)
* [Mouvements composite](gestures.md#composite-gestures) ([Tapped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.tapped.aspx), maintenez la touche, Manipulation, Navigation), accessible à l’aide un [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx)

### <a name="selectmenugrasptouchpadthumbstick-interactions-spatialinteractionmanager"></a>Sélectionnez/Menu/appréhendé/pavé tactile/stick analogique interactions : SpatialInteractionManager

Pour détecter les activations de bas niveau, des versions et mises à jour entre les mains et les périphériques d’entrée dans Windows Mixed Reality, vous démarrez à partir d’un [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx). Le SpatialInteractionManager dispose d’un événement qui signale à l’application lors de la main ou contrôleur de mouvement a détecté l’entrée.

Il existe trois types de clés de SpatialInteractionSource, chacun représenté par une autre valeur SpatialInteractionSourceKind :
* **Main** représente main détectés d’un utilisateur. Sources de main sont disponibles uniquement sur HoloLens.
* **Contrôleur** représente un contrôleur de mouvement associé. Contrôleurs de mouvement peuvent offrir un éventail de fonctionnalités, par exemple : Sélectionnez les déclencheurs, les boutons de Menu, des boutons de compréhension, pavés tactiles et sticks analogiques.
* **Voix** représente la voix de l’utilisateur à propos du système a détecté les mots clés. Cela injecter l’appui sur une sélection et mise en production chaque fois que l’utilisateur dit « Select ».

Pour détecter les appuis sur tous les types de ces sources d’interaction, vous pouvez gérer l’événement SourcePressed sur SpatialInteractionManager dans SpatialInputHandler.cpp :


```cpp
m_interactionManager = SpatialInteractionManager::GetForCurrentView();
    
// Bind a handler to the SourcePressed event.
m_sourcePressedEventToken =
    m_interactionManager->SourcePressed +=
        ref new TypedEventHandler<SpatialInteractionManager^, SpatialInteractionSourceEventArgs^>(
            bind(&SpatialInputHandler::OnSourcePressed, this, _1, _2)
            );
```

Cet événement appuyé est envoyé à votre application de manière asynchrone. Votre application ou le moteur de jeu souhaitez peut-être effectuer un traitement immédiatement, ou vous souhaiterez peut-être les données d’événement dans votre routine de traitement des entrées de file d’attente.

Le modèle inclut une classe d’assistance pour vous aider à démarrer. Ce modèle renonce à tout traitement par souci de simplicité de conception. La classe d’assistance qui effectue le suivi de si un ou plusieurs **Pressed** événements se sont produits depuis le dernier **mise à jour** appeler. À partir de SpatialInputHandler.cpp :




```cpp
void SpatialInputHandler::OnSourcePressed(SpatialInteractionManager^ sender, SpatialInteractionSourceEventArgs^ args)
{
    m_sourceState = args->State;
    
    //
    // TODO: In your app or game engine, rewrite this method to queue
    //       input events in your input class or event handler.
    //
}
```

Si, par conséquent, elle retourne le [SpatialInteractionSourceState](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) pour l’événement d’entrée le plus récent au cours de la prochaine mise à jour. À partir de SpatialInputHandler.cpp :




```cpp
// Checks if the user performed an input gesture since the last call to this method.
// Allows the main update loop to check for asynchronous changes to the user
// input state.
SpatialInteractionSourceState^ SpatialInputHandler::CheckForInput()
{
    SpatialInteractionSourceState^ sourceState = m_sourceState;
    m_sourceState = nullptr;
    return sourceState;
}
```

Notez que le code ci-dessus traitera tous appuie sur la même façon, si l’utilisateur exécute un réplica principal **sélectionnez** press ou une base de données secondaire **Menu** ou **saisir** appuyez sur. Le **sélectionnez** press est une forme principale d’interaction pris en charge entre les mains, motion contrôleurs et voix, déclenchées soit par une main effectuant un appui, un contrôleur de mouvements avec son déclencheur principal/bouton enfoncé ou l’utilisateur vocale indiquant que « Select ». Sélectionnez appuie sur représente l’intention de l’utilisateur pour activer l’hologramme que cibler.

Pour examiner le type de presse se produit, nous allons modifier le Gestionnaire d’événements SpatialInteractionManager::SourceUpdated. Notre code détecte des pressions de compréhension (le cas échéant) et utilisez-les pour repositionner le cube. Si appréhendé n’est pas disponible, nous utiliserons les appuis sélectionnez à la place.

Ajoutez les déclarations de membre privé suivantes à SpatialInputHandler.h : 


```cpp
void OnSourceUpdated(
       Windows::UI::Input::Spatial::SpatialInteractionManager^ sender,
       Windows::UI::Input::Spatial::SpatialInteractionSourceEventArgs^ args);
   Windows::Foundation::EventRegistrationToken m_sourceUpdatedEventToken;
```

Ouvrez SpatialInputHandler.cpp. Ajoutez l’inscription d’événement suivant au constructeur : 


```cpp
m_sourceUpdatedEventToken =
       m_interactionManager->SourceUpdated +=
       ref new TypedEventHandler<SpatialInteractionManager^, SpatialInteractionSourceEventArgs^>(
           bind(&SpatialInputHandler::OnSourceUpdated, this, _1, _2)
           );
```

Il s’agit du code de gestionnaire d’événements. Si la source d’entrée rencontre une compréhension, la pose de pointeur est stockée pour la boucle de mise à jour suivante. Sinon, il recherchera appui sur une sélection à la place. À partir de SpatialInputHandler.cpp :




```cpp
void SpatialInputHandler::OnSourceUpdated(SpatialInteractionManager^ sender, SpatialInteractionSourceEventArgs^ args)
{
    if (args->State->Source->IsGraspSupported)
    {
        if (args->State->IsGrasped)
        {
            m_sourceState = args->State;
        }
    }
    else
    {
        if (args->State->IsSelectPressed)
        {
            m_sourceState = args->State;
        }
    }
}
```

Veillez à annuler l’inscription du Gestionnaire d’événements dans le destructeur. À partir de SpatialInputHandler.cpp :


```cpp
m_interactionManager->SourceUpdated -= m_sourcePressedEventToken;
```

Recompiler et redéployer. Votre projet de modèle doit maintenant être en mesure de reconnaître la compréhension des interactions à repositionner le cube en rotation.

L’API SpatialInteractionSource prend en charge les contrôleurs avec un large éventail de fonctionnalités. Dans l’exemple ci-dessus, nous vérifions si appréhendé est pris en charge avant d’essayer de l’utiliser. Le SpatialInteractionSource prend en charge les fonctionnalités facultatives suivantes au-delà courantes **sélectionnez** appuyez sur :
* **Bouton de menu :** Vérifiez la prise en charge en inspectant la propriété IsMenuSupported. Lors de la prise en charge, consultez le [SpatialInteractionSourceState::IsMenuPressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) propriété pour déterminer si le bouton de menu est enfoncée.
* **Comprendre le bouton :** Vérifiez la prise en charge en inspectant la propriété IsGraspSupported. Lors de la prise en charge, consultez le [SpatialInteractionSourceState::IsGrasped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) propriété pour savoir si appréhendé est activé.

Pour les contrôleurs, le SpatialInteractionSource a une propriété de contrôleur avec des fonctionnalités supplémentaires.
* **HasThumbstick :** Si la valeur est true, le contrôleur a un stick analogique. Inspecter le [ControllerProperties](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractioncontrollerproperties) propriété de la SpatialInteractionSourceState pour acquérir le stick analogique x et les valeurs y (ThumbstickX et ThumbstickY), ainsi que son état enfoncé (IsThumbstickPressed).
* **HasTouchpad :** Si la valeur est true, le contrôleur a un pavé tactile. Inspecter la propriété ControllerProperties de la SpatialInteractionSourceState pour acquérir le pavé tactile x et y valeurs (TouchpadX et TouchpadY) et pour savoir si l’utilisateur touche le panneau (IsTouchpadTouched) et si elles sont en appuyant sur le pavé tactile vers le bas () IsTouchpadPressed).
* **SimpleHapticsController :** L’API SimpleHapticsController pour le contrôleur vous permet d’inspecter les fonctionnalités HAPTIQUES du contrôleur de, et il vous permet également de contrôler le retour haptique.

Notez que la plage pour le pavé tactile et stick analogique comprise entre -1 et 1 pour les deux axes (de bas en haut et de gauche à droite). La plage pour le déclencheur analogique, qui est accessible à l’aide de la propriété SpatialInteractionSourceState::SelectPressedValue, a une plage de 0 à 1. Une valeur de 1 met en corrélation avec IsSelectPressed étant égal à true ; toute autre valeur met en corrélation avec IsSelectPressed étant égal à false.

Notez que pour une main et un contrôleur, à l’aide de SpatialInteractionSourceState::Properties::TryGetLocation fournira la position de main de l’utilisateur est différente de la pose de pointeur représentant le rayon de pointage du contrôleur. Si vous souhaitez dessiner un élément à l’emplacement de la main, utilisez TryGetLocation. Si vous souhaitez raycast entre l’extrémité du contrôleur, obtenir le rayon de pointage à partir de TryGetInteractionSourcePose sur le SpatialPointerPose.

Vous pouvez également utiliser les autres événements sur SpatialInteractionManager, telles que SourceDetected et SourceLost, pour réagir quand mains entrent ou laisser l’appareil quand ils se déplacent dans ou hors de la position de prête (votre index déclenché avec palm vers l’avant) ou vue, ou lorsque de mouvement contrôleurs sont activées/désactivée ou sont appariés/apparié.

### <a name="grip-pose-vs-pointing-pose"></a>Pose de poignée et pose de pointage

Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.

Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser que vous pouvez examiner pour chaque source de l’interaction :
* Le **pose de poignée**, représentant l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.
    * Sur des casques IMMERSIFS, cette pose mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons.
    * Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée.
    * Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)
    * Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.
    * Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.
    * Vous pouvez accéder à la pose de poignée via [SpatialInteractionSourceState.Properties.TryGetLocation(...) ](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourceproperties#Windows_UI_Input_Spatial_SpatialInteractionSourceProperties_TryGetLocation_Windows_Perception_Spatial_SpatialCoordinateSystem_).
* Le **pose de pointeur**, qui représente l’info-bulle du contrôleur qui pointe vers l’avant.
    * Cette pose est mieux utilisé pour raycast lorsque **vers l’interface utilisateur** lorsque vous restituez le modèle de contrôleur lui-même.
    * Vous pouvez accéder à la pose de pointeur via [SpatialInteractionSourceState.Properties.TryGetLocation(...). SourcePointerPose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation#Windows_UI_Input_Spatial_SpatialInteractionSourceLocation_SourcePointerPose) ou [SpatialInteractionSourceState.TryGetPointerPose(...). TryGetInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose#Windows_UI_Input_Spatial_SpatialPointerPose_TryGetInteractionSourcePose_Windows_UI_Input_Spatial_SpatialInteractionSource_).

### <a name="composite-gestures-spatialgesturerecognizer"></a>Mouvements composite : SpatialGestureRecognizer

Un [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx) interprète les interactions de l’utilisateur à partir de mains, les contrôleurs de mouvement et la commande « Sélectionner » de la voix à des événements de mouvement spatial aire de conception, qui cible les utilisateurs à l’aide de leurs regards principal.

Mouvements spatiales constituent une forme de clé d’entrée pour les applications de réalité mixte de Windows. En routage d’interactions à partir de la SpatialInteractionManager à SpatialGestureRecognizer d’un hologramme, applications peuvent détecter les événements Tap, blocage, la Manipulation et Navigation uniformément entre les mains, voix et périphériques d’entrée spatiales, sans avoir à gérer les activations et libère manuellement.

SpatialGestureRecognizer effectue uniquement la levée d’ambiguïté minimale entre l’ensemble des gestes que vous demandez. Par exemple, si vous demandez simplement Tap, l’utilisateur peut maintenez son doigt en tant qu’ils le souhaitent et un drainage se produira toujours. Si vous demandez à la fois maintenez sur, après environ une seconde d’enfoncée son doigt, promeut le mouvement à une suspension et un drainage ne se produit plus.

Pour utiliser SpatialGestureRecognizer, gérer la SpatialInteractionManager [InteractionDetected](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialInteractionManager.InteractionDetected) événements et capture le SpatialPointerPose exposée il. Utilisez ray regards principal de l’utilisateur à partir de cette pose à croiser avec l’hologrammes et surface mailles dans son environnement de l’utilisateur, afin de déterminer ce que l’utilisateur a l’intention d’interagir avec. Ensuite, acheminer la SpatialInteraction dans les arguments d’événement pour SpatialGestureRecognizer de hologramme de cible, à l’aide de son [CaptureInteraction](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.CaptureInteraction) (méthode). Cela démarre l’interprétation de cette interaction conformément à la [SpatialGestureSettings](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureSettings) définies sur ce module de reconnaissance à l’heure de création - ou en [TrySetGestureSettings](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.TrySetGestureSettings).

Sur HoloLens, interactions et des mouvements doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la main. Une fois démarrée, une interaction des mouvements relatifs de la main peuvent servir à contrôler le mouvement, comme avec le mouvement de Manipulation ou de Navigation.

## <a name="see-also"></a>Voir aussi
* [Gaze](gaze.md)
* [Mouvements](gestures.md)
* [Contrôleurs de mouvement](motion-controllers.md)
