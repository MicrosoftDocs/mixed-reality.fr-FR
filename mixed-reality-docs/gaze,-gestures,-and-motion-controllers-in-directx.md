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
# <a name="gaze-gestures-and-motion-controllers-in-directx"></a><span data-ttu-id="3b726-104">Regards, les mouvements et les contrôleurs de mouvement dans DirectX</span><span class="sxs-lookup"><span data-stu-id="3b726-104">Gaze, gestures, and motion controllers in DirectX</span></span>

<span data-ttu-id="3b726-105">Si vous vous apprêtez à générer directement sur la plateforme, vous devrez gérer l’entrée provenant de l’utilisateur, tels que recherche où l’utilisateur [regards principal](gaze.md) et ce que l’utilisateur a sélectionné avec [mouvements](gestures.md) ou [contrôleurs de mouvement](motion-controllers.md).</span><span class="sxs-lookup"><span data-stu-id="3b726-105">If you're going to build directly on top of the platform, you will have to handle input coming from the user - such as where the user is looking via [head gaze](gaze.md) and what the user has selected with [gestures](gestures.md) or [motion controllers](motion-controllers.md).</span></span> <span data-ttu-id="3b726-106">Combinaison de ces formes de saisie, vous pouvez activer un utilisateur pour placer un [hologramme](hologram.md) dans votre application.</span><span class="sxs-lookup"><span data-stu-id="3b726-106">Combining these forms of input, you can enable a user to place a [hologram](hologram.md) in your app.</span></span> <span data-ttu-id="3b726-107">Le [modèle d’application HOLOGRAPHIQUE](creating-a-holographic-directx-project.md) a un exemple facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="3b726-107">The [holographic app template](creating-a-holographic-directx-project.md) has an easy to use example.</span></span>

>[!NOTE]
><span data-ttu-id="3b726-108">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="3b726-108">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="3b726-109">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="3b726-109">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="gaze-input"></a><span data-ttu-id="3b726-110">Entrée avec le pointage du regard</span><span class="sxs-lookup"><span data-stu-id="3b726-110">Gaze input</span></span>

<span data-ttu-id="3b726-111">Pour accéder à l’utilisateur [regards principal](gaze.md), vous utilisez le [SpatialPointerPose](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialpointerpose.aspx) type.</span><span class="sxs-lookup"><span data-stu-id="3b726-111">To access the user's [head gaze](gaze.md), you use the [SpatialPointerPose](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialpointerpose.aspx) type.</span></span> <span data-ttu-id="3b726-112">Le modèle d’application HOLOGRAPHIQUE inclut le code de base pour les regards de présentation.</span><span class="sxs-lookup"><span data-stu-id="3b726-112">The holographic app template includes basic code for understanding gaze.</span></span> <span data-ttu-id="3b726-113">Ce code fournit un vecteur qui pointe vers l’avant entre les yeux de l’utilisateur, compte tenu de position de l’appareil et l’orientation dans une donnée [système de coordonnées](coordinate-systems-in-directx.md).</span><span class="sxs-lookup"><span data-stu-id="3b726-113">This code provides a vector pointing forward from between the user's eyes, taking into account the device's position and orientation in a given [coordinate system](coordinate-systems-in-directx.md).</span></span>




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

<span data-ttu-id="3b726-114">Vous trouverez peut-être vous demandez : « Mais d'où provient le système de coordonnées ? »</span><span class="sxs-lookup"><span data-stu-id="3b726-114">You may find yourself asking: "But where does the coordinate system come from?"</span></span>

<span data-ttu-id="3b726-115">Nous allons répondre à cette question.</span><span class="sxs-lookup"><span data-stu-id="3b726-115">Let's answer that question.</span></span> <span data-ttu-id="3b726-116">Dans de notre AppMain **mise à jour** (fonction), nous traité un événement d’entrée spatial en acquérant par rapport à système de coordonnées pour notre StationaryFrameOfReference.</span><span class="sxs-lookup"><span data-stu-id="3b726-116">In our AppMain's **Update** function, we processed a spatial input event by acquiring it relative to the coordinate system for our StationaryFrameOfReference.</span></span> <span data-ttu-id="3b726-117">Rappelez-vous que le StationaryFrameOfReference a été créé lorsque nous configurons le [HolographicSpace](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx), et le système de coordonnées a été acquis au début de [mise à jour](rendering-in-directx.md).</span><span class="sxs-lookup"><span data-stu-id="3b726-117">Recall that the StationaryFrameOfReference was created when we set up the [HolographicSpace](https://msdn.microsoft.com/library/windows/apps/windows.graphics.holographic.holographicspace.aspx), and the coordinate system was acquired at the start of [Update](rendering-in-directx.md).</span></span>




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

<span data-ttu-id="3b726-118">Notez que les données sont liées à un état de pointeur quelconque.</span><span class="sxs-lookup"><span data-stu-id="3b726-118">Note that the data is tied to a pointer state of some kind.</span></span> <span data-ttu-id="3b726-119">Nous l’obtenir à partir d’un événement d’entrée spatial.</span><span class="sxs-lookup"><span data-stu-id="3b726-119">We get this from a spatial input event.</span></span> <span data-ttu-id="3b726-120">L’objet de données d’événement inclut un système de coordonnées, afin que vous pouvez toujours associer la direction du regard au moment de l’événement à quelque système de coordonnées spatial vous avez besoin.</span><span class="sxs-lookup"><span data-stu-id="3b726-120">The event data object includes a coordinate system, so that you can always relate the gaze direction at the time of the event to whatever spatial coordinate system you need.</span></span> <span data-ttu-id="3b726-121">En fait, vous devez le faire afin d’obtenir la pose de pointeur.</span><span class="sxs-lookup"><span data-stu-id="3b726-121">In fact, you must do so in order to get the pointer pose.</span></span>

> [!NOTE]
> <span data-ttu-id="3b726-122">Obtenir des instructions spécifiques pour HoloLens 2 [bientôt](index.md#news-and-notes).</span><span class="sxs-lookup"><span data-stu-id="3b726-122">More guidance specific to HoloLens 2 [coming soon](index.md#news-and-notes).</span></span>

## <a name="gesture-and-motion-controller-input"></a><span data-ttu-id="3b726-123">Contrôleur de mouvement et le mouvement d’entrée</span><span class="sxs-lookup"><span data-stu-id="3b726-123">Gesture and motion controller input</span></span>

<span data-ttu-id="3b726-124">En réalité mixte de Windows, les deux main [mouvements](gestures.md) et [contrôleurs de mouvement](motion-controllers.md) sont gérées via la même entrée spatiale API, trouvée dans le [Windows.UI.Input.Spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial) espace de noms.</span><span class="sxs-lookup"><span data-stu-id="3b726-124">In Windows Mixed Reality, both hand [gestures](gestures.md) and [motion controllers](motion-controllers.md) are handled through the same spatial input APIs, found in the [Windows.UI.Input.Spatial](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial) namespace.</span></span> <span data-ttu-id="3b726-125">Cela vous permet de gérer facilement des actions courantes telles que **sélectionnez** appuie sur la même façon entre les mains et contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="3b726-125">This enables you to easily handle common actions like **Select** presses the same way across both hands and motion controllers.</span></span>

<span data-ttu-id="3b726-126">Il existe deux niveaux d’API, vous pouvez cibler lors de la gestion des contrôleurs de mouvement ou de mouvements en réalité mixte :</span><span class="sxs-lookup"><span data-stu-id="3b726-126">There are two levels of API you can target when handling gestures or motion controllers in mixed reality:</span></span>
* <span data-ttu-id="3b726-127">[Interactions](gestures.md#the-two-core-gestures-of-hololens) ([SourcePressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed.aspx), [SourceReleased](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased.aspx) et [SourceUpdated](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated.aspx)), accessible à l’aide un [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx)</span><span class="sxs-lookup"><span data-stu-id="3b726-127">[Interactions](gestures.md#the-two-core-gestures-of-hololens) ([SourcePressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcepressed.aspx), [SourceReleased](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourcereleased.aspx) and [SourceUpdated](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.sourceupdated.aspx)), accessed using a [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx)</span></span>
* <span data-ttu-id="3b726-128">[Mouvements composite](gestures.md#composite-gestures) ([Tapped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.tapped.aspx), maintenez la touche, Manipulation, Navigation), accessible à l’aide un [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx)</span><span class="sxs-lookup"><span data-stu-id="3b726-128">[Composite gestures](gestures.md#composite-gestures) ([Tapped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.tapped.aspx), Hold, Manipulation, Navigation), accessed using a [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx)</span></span>

### <a name="selectmenugrasptouchpadthumbstick-interactions-spatialinteractionmanager"></a><span data-ttu-id="3b726-129">Sélectionnez/Menu/appréhendé/pavé tactile/stick analogique interactions : SpatialInteractionManager</span><span class="sxs-lookup"><span data-stu-id="3b726-129">Select/Menu/Grasp/Touchpad/Thumbstick interactions: SpatialInteractionManager</span></span>

<span data-ttu-id="3b726-130">Pour détecter les activations de bas niveau, des versions et mises à jour entre les mains et les périphériques d’entrée dans Windows Mixed Reality, vous démarrez à partir d’un [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="3b726-130">To detect low-level presses, releases and updates across hands and input devices in Windows Mixed Reality, you start from a [SpatialInteractionManager](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionmanager.aspx).</span></span> <span data-ttu-id="3b726-131">Le SpatialInteractionManager dispose d’un événement qui signale à l’application lors de la main ou contrôleur de mouvement a détecté l’entrée.</span><span class="sxs-lookup"><span data-stu-id="3b726-131">The SpatialInteractionManager has an event that informs the app when a hand or motion controller has detected input.</span></span>

<span data-ttu-id="3b726-132">Il existe trois types de clés de SpatialInteractionSource, chacun représenté par une autre valeur SpatialInteractionSourceKind :</span><span class="sxs-lookup"><span data-stu-id="3b726-132">There are three key kinds of SpatialInteractionSource, each represented by a different SpatialInteractionSourceKind value:</span></span>
* <span data-ttu-id="3b726-133">**Main** représente main détectés d’un utilisateur.</span><span class="sxs-lookup"><span data-stu-id="3b726-133">**Hand** represents a user's detected hand.</span></span> <span data-ttu-id="3b726-134">Sources de main sont disponibles uniquement sur HoloLens.</span><span class="sxs-lookup"><span data-stu-id="3b726-134">Hand sources are available only on HoloLens.</span></span>
* <span data-ttu-id="3b726-135">**Contrôleur** représente un contrôleur de mouvement associé.</span><span class="sxs-lookup"><span data-stu-id="3b726-135">**Controller** represents a paired motion controller.</span></span> <span data-ttu-id="3b726-136">Contrôleurs de mouvement peuvent offrir un éventail de fonctionnalités, par exemple : Sélectionnez les déclencheurs, les boutons de Menu, des boutons de compréhension, pavés tactiles et sticks analogiques.</span><span class="sxs-lookup"><span data-stu-id="3b726-136">Motion controllers can offer a variety of capabilities, for example: Select triggers, Menu buttons, Grasp buttons, touchpads and thumbsticks.</span></span>
* <span data-ttu-id="3b726-137">**Voix** représente la voix de l’utilisateur à propos du système a détecté les mots clés.</span><span class="sxs-lookup"><span data-stu-id="3b726-137">**Voice** represents the user's voice speaking system-detected keywords.</span></span> <span data-ttu-id="3b726-138">Cela injecter l’appui sur une sélection et mise en production chaque fois que l’utilisateur dit « Select ».</span><span class="sxs-lookup"><span data-stu-id="3b726-138">This will inject a Select press and release whenever the user says "Select".</span></span>

<span data-ttu-id="3b726-139">Pour détecter les appuis sur tous les types de ces sources d’interaction, vous pouvez gérer l’événement SourcePressed sur SpatialInteractionManager dans SpatialInputHandler.cpp :</span><span class="sxs-lookup"><span data-stu-id="3b726-139">To detect presses across any of these interaction sources, you can handle the SourcePressed event on SpatialInteractionManager in SpatialInputHandler.cpp:</span></span>


```cpp
m_interactionManager = SpatialInteractionManager::GetForCurrentView();
    
// Bind a handler to the SourcePressed event.
m_sourcePressedEventToken =
    m_interactionManager->SourcePressed +=
        ref new TypedEventHandler<SpatialInteractionManager^, SpatialInteractionSourceEventArgs^>(
            bind(&SpatialInputHandler::OnSourcePressed, this, _1, _2)
            );
```

<span data-ttu-id="3b726-140">Cet événement appuyé est envoyé à votre application de manière asynchrone.</span><span class="sxs-lookup"><span data-stu-id="3b726-140">This pressed event is sent to your app asynchronously.</span></span> <span data-ttu-id="3b726-141">Votre application ou le moteur de jeu souhaitez peut-être effectuer un traitement immédiatement, ou vous souhaiterez peut-être les données d’événement dans votre routine de traitement des entrées de file d’attente.</span><span class="sxs-lookup"><span data-stu-id="3b726-141">Your app or game engine may want to perform some processing right away or you may want to queue up the event data in your input processing routine.</span></span>

<span data-ttu-id="3b726-142">Le modèle inclut une classe d’assistance pour vous aider à démarrer.</span><span class="sxs-lookup"><span data-stu-id="3b726-142">The template includes a helper class to get you started.</span></span> <span data-ttu-id="3b726-143">Ce modèle renonce à tout traitement par souci de simplicité de conception.</span><span class="sxs-lookup"><span data-stu-id="3b726-143">This template forgoes any processing for simplicity of design.</span></span> <span data-ttu-id="3b726-144">La classe d’assistance qui effectue le suivi de si un ou plusieurs **Pressed** événements se sont produits depuis le dernier **mise à jour** appeler.</span><span class="sxs-lookup"><span data-stu-id="3b726-144">The helper class keeps track of whether one or more **Pressed** events occurred since the last **Update** call.</span></span> <span data-ttu-id="3b726-145">À partir de SpatialInputHandler.cpp :</span><span class="sxs-lookup"><span data-stu-id="3b726-145">From SpatialInputHandler.cpp:</span></span>




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

<span data-ttu-id="3b726-146">Si, par conséquent, elle retourne le [SpatialInteractionSourceState](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) pour l’événement d’entrée le plus récent au cours de la prochaine mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3b726-146">If so, it returns the [SpatialInteractionSourceState](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) for the most recent input event during the next Update.</span></span> <span data-ttu-id="3b726-147">À partir de SpatialInputHandler.cpp :</span><span class="sxs-lookup"><span data-stu-id="3b726-147">From SpatialInputHandler.cpp:</span></span>




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

<span data-ttu-id="3b726-148">Notez que le code ci-dessus traitera tous appuie sur la même façon, si l’utilisateur exécute un réplica principal **sélectionnez** press ou une base de données secondaire **Menu** ou **saisir** appuyez sur.</span><span class="sxs-lookup"><span data-stu-id="3b726-148">Note that the code above will treat all presses the same way, whether the user is performing a primary **Select** press or a secondary **Menu** or **Grasp** press.</span></span> <span data-ttu-id="3b726-149">Le **sélectionnez** press est une forme principale d’interaction pris en charge entre les mains, motion contrôleurs et voix, déclenchées soit par une main effectuant un appui, un contrôleur de mouvements avec son déclencheur principal/bouton enfoncé ou l’utilisateur vocale indiquant que « Select ».</span><span class="sxs-lookup"><span data-stu-id="3b726-149">The **Select** press is a primary form of interaction supported across hands, motion controllers and voice, triggered either by a hand performing an air-tap, a motion controller with its primary trigger/button pressed, or the user's voice saying "Select".</span></span> <span data-ttu-id="3b726-150">Sélectionnez appuie sur représente l’intention de l’utilisateur pour activer l’hologramme que cibler.</span><span class="sxs-lookup"><span data-stu-id="3b726-150">Select presses represent the user's intention to activate the hologram they are targeting.</span></span>

<span data-ttu-id="3b726-151">Pour examiner le type de presse se produit, nous allons modifier le Gestionnaire d’événements SpatialInteractionManager::SourceUpdated.</span><span class="sxs-lookup"><span data-stu-id="3b726-151">To reason about which kind of press is occurring, we will modify the SpatialInteractionManager::SourceUpdated event handler.</span></span> <span data-ttu-id="3b726-152">Notre code détecte des pressions de compréhension (le cas échéant) et utilisez-les pour repositionner le cube.</span><span class="sxs-lookup"><span data-stu-id="3b726-152">Our code will detect Grasp presses (where available) and use them to reposition the cube.</span></span> <span data-ttu-id="3b726-153">Si appréhendé n’est pas disponible, nous utiliserons les appuis sélectionnez à la place.</span><span class="sxs-lookup"><span data-stu-id="3b726-153">If Grasp is not available, we will use Select presses instead.</span></span>

<span data-ttu-id="3b726-154">Ajoutez les déclarations de membre privé suivantes à SpatialInputHandler.h :</span><span class="sxs-lookup"><span data-stu-id="3b726-154">Add the following private member declarations to SpatialInputHandler.h:</span></span> 


```cpp
void OnSourceUpdated(
       Windows::UI::Input::Spatial::SpatialInteractionManager^ sender,
       Windows::UI::Input::Spatial::SpatialInteractionSourceEventArgs^ args);
   Windows::Foundation::EventRegistrationToken m_sourceUpdatedEventToken;
```

<span data-ttu-id="3b726-155">Ouvrez SpatialInputHandler.cpp.</span><span class="sxs-lookup"><span data-stu-id="3b726-155">Open SpatialInputHandler.cpp.</span></span> <span data-ttu-id="3b726-156">Ajoutez l’inscription d’événement suivant au constructeur :</span><span class="sxs-lookup"><span data-stu-id="3b726-156">Add the following event registration to the constructor:</span></span> 


```cpp
m_sourceUpdatedEventToken =
       m_interactionManager->SourceUpdated +=
       ref new TypedEventHandler<SpatialInteractionManager^, SpatialInteractionSourceEventArgs^>(
           bind(&SpatialInputHandler::OnSourceUpdated, this, _1, _2)
           );
```

<span data-ttu-id="3b726-157">Il s’agit du code de gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="3b726-157">This is the event handler code.</span></span> <span data-ttu-id="3b726-158">Si la source d’entrée rencontre une compréhension, la pose de pointeur est stockée pour la boucle de mise à jour suivante.</span><span class="sxs-lookup"><span data-stu-id="3b726-158">If the input source is experiencing a Grasp, the pointer pose will be stored for the next update loop.</span></span> <span data-ttu-id="3b726-159">Sinon, il recherchera appui sur une sélection à la place.</span><span class="sxs-lookup"><span data-stu-id="3b726-159">Otherwise, it will check for a Select press instead.</span></span> <span data-ttu-id="3b726-160">À partir de SpatialInputHandler.cpp :</span><span class="sxs-lookup"><span data-stu-id="3b726-160">From SpatialInputHandler.cpp:</span></span>




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

<span data-ttu-id="3b726-161">Veillez à annuler l’inscription du Gestionnaire d’événements dans le destructeur.</span><span class="sxs-lookup"><span data-stu-id="3b726-161">Make sure to unregister the event handler in the destructor.</span></span> <span data-ttu-id="3b726-162">À partir de SpatialInputHandler.cpp :</span><span class="sxs-lookup"><span data-stu-id="3b726-162">From SpatialInputHandler.cpp:</span></span>


```cpp
m_interactionManager->SourceUpdated -= m_sourcePressedEventToken;
```

<span data-ttu-id="3b726-163">Recompiler et redéployer.</span><span class="sxs-lookup"><span data-stu-id="3b726-163">Recompile, and then redeploy.</span></span> <span data-ttu-id="3b726-164">Votre projet de modèle doit maintenant être en mesure de reconnaître la compréhension des interactions à repositionner le cube en rotation.</span><span class="sxs-lookup"><span data-stu-id="3b726-164">Your template project should now be able to recognize Grasp interactions to reposition the spinning cube.</span></span>

<span data-ttu-id="3b726-165">L’API SpatialInteractionSource prend en charge les contrôleurs avec un large éventail de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="3b726-165">The SpatialInteractionSource API supports controllers with a wide range of capabilities.</span></span> <span data-ttu-id="3b726-166">Dans l’exemple ci-dessus, nous vérifions si appréhendé est pris en charge avant d’essayer de l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="3b726-166">In the example shown above, we check to see if Grasp is supported before trying to use it.</span></span> <span data-ttu-id="3b726-167">Le SpatialInteractionSource prend en charge les fonctionnalités facultatives suivantes au-delà courantes **sélectionnez** appuyez sur :</span><span class="sxs-lookup"><span data-stu-id="3b726-167">The SpatialInteractionSource supports the following optional features beyond the common **Select** press:</span></span>
* <span data-ttu-id="3b726-168">**Bouton de menu :** Vérifiez la prise en charge en inspectant la propriété IsMenuSupported.</span><span class="sxs-lookup"><span data-stu-id="3b726-168">**Menu button:** Check support by inspecting the IsMenuSupported property.</span></span> <span data-ttu-id="3b726-169">Lors de la prise en charge, consultez le [SpatialInteractionSourceState::IsMenuPressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) propriété pour déterminer si le bouton de menu est enfoncée.</span><span class="sxs-lookup"><span data-stu-id="3b726-169">When supported, check the [SpatialInteractionSourceState::IsMenuPressed](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) property to find out if the menu button is pressed.</span></span>
* <span data-ttu-id="3b726-170">**Comprendre le bouton :** Vérifiez la prise en charge en inspectant la propriété IsGraspSupported.</span><span class="sxs-lookup"><span data-stu-id="3b726-170">**Grasp button:** Check support by inspecting the IsGraspSupported property.</span></span> <span data-ttu-id="3b726-171">Lors de la prise en charge, consultez le [SpatialInteractionSourceState::IsGrasped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) propriété pour savoir si appréhendé est activé.</span><span class="sxs-lookup"><span data-stu-id="3b726-171">When supported, check the [SpatialInteractionSourceState::IsGrasped](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialinteractionsourcestate.aspx) property to find out if grasp is activated.</span></span>

<span data-ttu-id="3b726-172">Pour les contrôleurs, le SpatialInteractionSource a une propriété de contrôleur avec des fonctionnalités supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="3b726-172">For controllers, the SpatialInteractionSource has a Controller property with additional capabilities.</span></span>
* <span data-ttu-id="3b726-173">**HasThumbstick :** Si la valeur est true, le contrôleur a un stick analogique.</span><span class="sxs-lookup"><span data-stu-id="3b726-173">**HasThumbstick:** If true, the controller has a thumbstick.</span></span> <span data-ttu-id="3b726-174">Inspecter le [ControllerProperties](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractioncontrollerproperties) propriété de la SpatialInteractionSourceState pour acquérir le stick analogique x et les valeurs y (ThumbstickX et ThumbstickY), ainsi que son état enfoncé (IsThumbstickPressed).</span><span class="sxs-lookup"><span data-stu-id="3b726-174">Inspect the [ControllerProperties](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractioncontrollerproperties) property of the SpatialInteractionSourceState to acquire the thumbstick x and y values (ThumbstickX and ThumbstickY), as well as its pressed state (IsThumbstickPressed).</span></span>
* <span data-ttu-id="3b726-175">**HasTouchpad :** Si la valeur est true, le contrôleur a un pavé tactile.</span><span class="sxs-lookup"><span data-stu-id="3b726-175">**HasTouchpad:** If true, the controller has a touchpad.</span></span> <span data-ttu-id="3b726-176">Inspecter la propriété ControllerProperties de la SpatialInteractionSourceState pour acquérir le pavé tactile x et y valeurs (TouchpadX et TouchpadY) et pour savoir si l’utilisateur touche le panneau (IsTouchpadTouched) et si elles sont en appuyant sur le pavé tactile vers le bas () IsTouchpadPressed).</span><span class="sxs-lookup"><span data-stu-id="3b726-176">Inspect the ControllerProperties property of the SpatialInteractionSourceState to acquire the touchpad x and y values (TouchpadX and TouchpadY), and to know if the user is touching the pad (IsTouchpadTouched) and if they are pressing the touchpad down (IsTouchpadPressed).</span></span>
* <span data-ttu-id="3b726-177">**SimpleHapticsController :** L’API SimpleHapticsController pour le contrôleur vous permet d’inspecter les fonctionnalités HAPTIQUES du contrôleur de, et il vous permet également de contrôler le retour haptique.</span><span class="sxs-lookup"><span data-stu-id="3b726-177">**SimpleHapticsController:** The SimpleHapticsController API for the controller allows you to inspect the haptics capabilities of the controller, and it also allows you to control haptic feedback.</span></span>

<span data-ttu-id="3b726-178">Notez que la plage pour le pavé tactile et stick analogique comprise entre -1 et 1 pour les deux axes (de bas en haut et de gauche à droite).</span><span class="sxs-lookup"><span data-stu-id="3b726-178">Note that the range for touchpad and thumbstick from -1 to 1 for both axes (from bottom to top, and from left to right).</span></span> <span data-ttu-id="3b726-179">La plage pour le déclencheur analogique, qui est accessible à l’aide de la propriété SpatialInteractionSourceState::SelectPressedValue, a une plage de 0 à 1.</span><span class="sxs-lookup"><span data-stu-id="3b726-179">The range for the analog trigger, which is accessed using the SpatialInteractionSourceState::SelectPressedValue property, has a range of 0 to 1.</span></span> <span data-ttu-id="3b726-180">Une valeur de 1 met en corrélation avec IsSelectPressed étant égal à true ; toute autre valeur met en corrélation avec IsSelectPressed étant égal à false.</span><span class="sxs-lookup"><span data-stu-id="3b726-180">A value of 1 correlates with IsSelectPressed being equal to true; any other value correlates with IsSelectPressed being equal to false.</span></span>

<span data-ttu-id="3b726-181">Notez que pour une main et un contrôleur, à l’aide de SpatialInteractionSourceState::Properties::TryGetLocation fournira la position de main de l’utilisateur est différente de la pose de pointeur représentant le rayon de pointage du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="3b726-181">Note that for both a hand and a controller, using SpatialInteractionSourceState::Properties::TryGetLocation will provide the user's hand position - this is distinct from the pointer pose representing the controller's pointing ray.</span></span> <span data-ttu-id="3b726-182">Si vous souhaitez dessiner un élément à l’emplacement de la main, utilisez TryGetLocation.</span><span class="sxs-lookup"><span data-stu-id="3b726-182">If you want to draw something at the hand location, use TryGetLocation.</span></span> <span data-ttu-id="3b726-183">Si vous souhaitez raycast entre l’extrémité du contrôleur, obtenir le rayon de pointage à partir de TryGetInteractionSourcePose sur le SpatialPointerPose.</span><span class="sxs-lookup"><span data-stu-id="3b726-183">If you want to raycast from the tip of the controller, get the pointing ray from TryGetInteractionSourcePose on the SpatialPointerPose.</span></span>

<span data-ttu-id="3b726-184">Vous pouvez également utiliser les autres événements sur SpatialInteractionManager, telles que SourceDetected et SourceLost, pour réagir quand mains entrent ou laisser l’appareil quand ils se déplacent dans ou hors de la position de prête (votre index déclenché avec palm vers l’avant) ou vue, ou lorsque de mouvement contrôleurs sont activées/désactivée ou sont appariés/apparié.</span><span class="sxs-lookup"><span data-stu-id="3b726-184">You can also use the other events on SpatialInteractionManager, such as SourceDetected and SourceLost, to react when hands enter or leave the device's view or when they move in or out of the ready position (index finger raised with palm forward), or when motion controllers are turned on/off or are paired/unpaired.</span></span>

### <a name="grip-pose-vs-pointing-pose"></a><span data-ttu-id="3b726-185">Pose de poignée et pose de pointage</span><span class="sxs-lookup"><span data-stu-id="3b726-185">Grip pose vs. pointing pose</span></span>

<span data-ttu-id="3b726-186">Réalité mixte Windows prend en charge les contrôleurs de mouvements dans un large éventail de facteurs de forme, avec la conception de chaque contrôleur qui se différencie par sa relation entre la position des utilisateurs manuellement et naturel « transférer » direction que les applications doit utiliser pour le pointage lors du rendu de la contrôleur.</span><span class="sxs-lookup"><span data-stu-id="3b726-186">Windows Mixed Reality supports motion controllers in a variety of form factors, with each controller's design differing in its relationship between the user's hand position and the natural "forward" direction that apps should use for pointing when rendering the controller.</span></span>

<span data-ttu-id="3b726-187">Pour mieux représenter ces contrôleurs, il existe deux types de risque de poser que vous pouvez examiner pour chaque source de l’interaction :</span><span class="sxs-lookup"><span data-stu-id="3b726-187">To better represent these controllers, there are two kinds of poses you can investigate for each interaction source:</span></span>
* <span data-ttu-id="3b726-188">Le **pose de poignée**, représentant l’emplacement de la portée de main détectée par un HoloLens ou palm contenant un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="3b726-188">The **grip pose**, representing the location of either the palm of a hand detected by a HoloLens, or the palm holding a motion controller.</span></span>
    * <span data-ttu-id="3b726-189">Sur des casques IMMERSIFS, cette pose mieux permet de restituer **main de l’utilisateur** ou **détenues par un objet à portée de main de l’utilisateur**, tel qu’un mot de passe ou les électrons.</span><span class="sxs-lookup"><span data-stu-id="3b726-189">On immersive headsets, this pose is best used to render **the user's hand** or **an object held in the user's hand**, such as a sword or gun.</span></span>
    * <span data-ttu-id="3b726-190">Le **Attrapez position**: Le centroïde de palm naturellement, tout en maintenant le contrôleur ajustée gauche ou droite pour centrer la position au sein de la poignée.</span><span class="sxs-lookup"><span data-stu-id="3b726-190">The **grip position**: The palm centroid when holding the controller naturally, adjusted left or right to center the position within the grip.</span></span>
    * <span data-ttu-id="3b726-191">Le **Attrapez axe de droite de l’orientation**: Lorsque vous ouvrez totalement la main pour former une pose plat 5-doigt, le rayon qui est normal pour votre palm (en avant à partir de la gauche palm, vers l’arrière de palm droite)</span><span class="sxs-lookup"><span data-stu-id="3b726-191">The **grip orientation's Right axis**: When you completely open your hand to form a flat 5-finger pose, the ray that is normal to your palm (forward from left palm, backward from right palm)</span></span>
    * <span data-ttu-id="3b726-192">Le **Attrapez axe vers l’avant de l’orientation**: Lorsque vous fermez votre main partiellement (comme le cas maintenant le contrôleur), le rayon pointe « forward » via le tube formé par vos doigts non curseur.</span><span class="sxs-lookup"><span data-stu-id="3b726-192">The **grip orientation's Forward axis**: When you close your hand partially (as if holding the controller), the ray that points "forward" through the tube formed by your non-thumb fingers.</span></span>
    * <span data-ttu-id="3b726-193">Le **Attrapez orientation d’axe**: L’axe à distance impliqué par les définitions de droite, en avant.</span><span class="sxs-lookup"><span data-stu-id="3b726-193">The **grip orientation's Up axis**: The Up axis implied by the Right and Forward definitions.</span></span>
    * <span data-ttu-id="3b726-194">Vous pouvez accéder à la pose de poignée via [SpatialInteractionSourceState.Properties.TryGetLocation(...) ](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourceproperties#Windows_UI_Input_Spatial_SpatialInteractionSourceProperties_TryGetLocation_Windows_Perception_Spatial_SpatialCoordinateSystem_).</span><span class="sxs-lookup"><span data-stu-id="3b726-194">You can access the grip pose through [SpatialInteractionSourceState.Properties.TryGetLocation(...)](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourceproperties#Windows_UI_Input_Spatial_SpatialInteractionSourceProperties_TryGetLocation_Windows_Perception_Spatial_SpatialCoordinateSystem_).</span></span>
* <span data-ttu-id="3b726-195">Le **pose de pointeur**, qui représente l’info-bulle du contrôleur qui pointe vers l’avant.</span><span class="sxs-lookup"><span data-stu-id="3b726-195">The **pointer pose**, representing the tip of the controller pointing forward.</span></span>
    * <span data-ttu-id="3b726-196">Cette pose est mieux utilisé pour raycast lorsque **vers l’interface utilisateur** lorsque vous restituez le modèle de contrôleur lui-même.</span><span class="sxs-lookup"><span data-stu-id="3b726-196">This pose is best used to raycast when **pointing at UI** when you are rendering the controller model itself.</span></span>
    * <span data-ttu-id="3b726-197">Vous pouvez accéder à la pose de pointeur via [SpatialInteractionSourceState.Properties.TryGetLocation(...). SourcePointerPose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation#Windows_UI_Input_Spatial_SpatialInteractionSourceLocation_SourcePointerPose) ou [SpatialInteractionSourceState.TryGetPointerPose(...). TryGetInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose#Windows_UI_Input_Spatial_SpatialPointerPose_TryGetInteractionSourcePose_Windows_UI_Input_Spatial_SpatialInteractionSource_).</span><span class="sxs-lookup"><span data-stu-id="3b726-197">You can access the pointer pose through [SpatialInteractionSourceState.Properties.TryGetLocation(...).SourcePointerPose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialinteractionsourcelocation#Windows_UI_Input_Spatial_SpatialInteractionSourceLocation_SourcePointerPose) or [SpatialInteractionSourceState.TryGetPointerPose(...).TryGetInteractionSourcePose](https://docs.microsoft.com/uwp/api/windows.ui.input.spatial.spatialpointerpose#Windows_UI_Input_Spatial_SpatialPointerPose_TryGetInteractionSourcePose_Windows_UI_Input_Spatial_SpatialInteractionSource_).</span></span>

### <a name="composite-gestures-spatialgesturerecognizer"></a><span data-ttu-id="3b726-198">Mouvements composite : SpatialGestureRecognizer</span><span class="sxs-lookup"><span data-stu-id="3b726-198">Composite gestures: SpatialGestureRecognizer</span></span>

<span data-ttu-id="3b726-199">Un [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx) interprète les interactions de l’utilisateur à partir de mains, les contrôleurs de mouvement et la commande « Sélectionner » de la voix à des événements de mouvement spatial aire de conception, qui cible les utilisateurs à l’aide de leurs regards principal.</span><span class="sxs-lookup"><span data-stu-id="3b726-199">A [SpatialGestureRecognizer](https://msdn.microsoft.com/library/windows/apps/windows.ui.input.spatial.spatialgesturerecognizer.aspx) interprets user interactions from hands, motion controllers, and the "Select" voice command to surface spatial gesture events, which users target using their head gaze.</span></span>

<span data-ttu-id="3b726-200">Mouvements spatiales constituent une forme de clé d’entrée pour les applications de réalité mixte de Windows.</span><span class="sxs-lookup"><span data-stu-id="3b726-200">Spatial gestures are a key form of input for Windows Mixed Reality apps.</span></span> <span data-ttu-id="3b726-201">En routage d’interactions à partir de la SpatialInteractionManager à SpatialGestureRecognizer d’un hologramme, applications peuvent détecter les événements Tap, blocage, la Manipulation et Navigation uniformément entre les mains, voix et périphériques d’entrée spatiales, sans avoir à gérer les activations et libère manuellement.</span><span class="sxs-lookup"><span data-stu-id="3b726-201">By routing interactions from the SpatialInteractionManager to a hologram's SpatialGestureRecognizer, apps can detect Tap, Hold, Manipulation, and Navigation events uniformly across hands, voice, and spatial input devices, without having to handle presses and releases manually.</span></span>

<span data-ttu-id="3b726-202">SpatialGestureRecognizer effectue uniquement la levée d’ambiguïté minimale entre l’ensemble des gestes que vous demandez.</span><span class="sxs-lookup"><span data-stu-id="3b726-202">SpatialGestureRecognizer performs only the minimal disambiguation between the set of gestures that you request.</span></span> <span data-ttu-id="3b726-203">Par exemple, si vous demandez simplement Tap, l’utilisateur peut maintenez son doigt en tant qu’ils le souhaitent et un drainage se produira toujours.</span><span class="sxs-lookup"><span data-stu-id="3b726-203">For example, if you request just Tap, the user may hold their finger down as long as they like and a Tap will still occur.</span></span> <span data-ttu-id="3b726-204">Si vous demandez à la fois maintenez sur, après environ une seconde d’enfoncée son doigt, promeut le mouvement à une suspension et un drainage ne se produit plus.</span><span class="sxs-lookup"><span data-stu-id="3b726-204">If you request both Tap and Hold, after about a second of holding down their finger, the gesture will promote to a Hold and a Tap will no longer occur.</span></span>

<span data-ttu-id="3b726-205">Pour utiliser SpatialGestureRecognizer, gérer la SpatialInteractionManager [InteractionDetected](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialInteractionManager.InteractionDetected) événements et capture le SpatialPointerPose exposée il.</span><span class="sxs-lookup"><span data-stu-id="3b726-205">To use SpatialGestureRecognizer, handle the SpatialInteractionManager's [InteractionDetected](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialInteractionManager.InteractionDetected) event and grab the SpatialPointerPose exposed there.</span></span> <span data-ttu-id="3b726-206">Utilisez ray regards principal de l’utilisateur à partir de cette pose à croiser avec l’hologrammes et surface mailles dans son environnement de l’utilisateur, afin de déterminer ce que l’utilisateur a l’intention d’interagir avec.</span><span class="sxs-lookup"><span data-stu-id="3b726-206">Use the user's head gaze ray from this pose to intersect with the holograms and surface meshes in the user's surroundings, in order to determine what the user is intending to interact with.</span></span> <span data-ttu-id="3b726-207">Ensuite, acheminer la SpatialInteraction dans les arguments d’événement pour SpatialGestureRecognizer de hologramme de cible, à l’aide de son [CaptureInteraction](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.CaptureInteraction) (méthode).</span><span class="sxs-lookup"><span data-stu-id="3b726-207">Then, route the SpatialInteraction in the event arguments to the target hologram's SpatialGestureRecognizer, using its [CaptureInteraction](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.CaptureInteraction) method.</span></span> <span data-ttu-id="3b726-208">Cela démarre l’interprétation de cette interaction conformément à la [SpatialGestureSettings](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureSettings) définies sur ce module de reconnaissance à l’heure de création - ou en [TrySetGestureSettings](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.TrySetGestureSettings).</span><span class="sxs-lookup"><span data-stu-id="3b726-208">This starts interpreting that interaction according to the [SpatialGestureSettings](https://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureSettings) set on that recognizer at creation time - or by [TrySetGestureSettings](http://msdn.microsoft.com/library/windows/apps/xaml/Windows.UI.Input.Spatial.SpatialGestureRecognizer.TrySetGestureSettings).</span></span>

<span data-ttu-id="3b726-209">Sur HoloLens, interactions et des mouvements doivent dériver généralement leur ciblage à partir des regards principal de l’utilisateur, au lieu d’essayer restituer ou interagir directement à l’emplacement de la main.</span><span class="sxs-lookup"><span data-stu-id="3b726-209">On HoloLens, interactions and gestures should generally derive their targeting from the user's head gaze, rather than trying to render or interact at the hand's location directly.</span></span> <span data-ttu-id="3b726-210">Une fois démarrée, une interaction des mouvements relatifs de la main peuvent servir à contrôler le mouvement, comme avec le mouvement de Manipulation ou de Navigation.</span><span class="sxs-lookup"><span data-stu-id="3b726-210">Once an interaction has started, relative motions of the hand may be used to control the gesture, as with the Manipulation or Navigation gesture.</span></span>

## <a name="see-also"></a><span data-ttu-id="3b726-211">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3b726-211">See also</span></span>
* [<span data-ttu-id="3b726-212">Gaze</span><span class="sxs-lookup"><span data-stu-id="3b726-212">Gaze</span></span>](gaze.md)
* [<span data-ttu-id="3b726-213">Mouvements</span><span class="sxs-lookup"><span data-stu-id="3b726-213">Gestures</span></span>](gestures.md)
* [<span data-ttu-id="3b726-214">Contrôleurs de mouvement</span><span class="sxs-lookup"><span data-stu-id="3b726-214">Motion controllers</span></span>](motion-controllers.md)
