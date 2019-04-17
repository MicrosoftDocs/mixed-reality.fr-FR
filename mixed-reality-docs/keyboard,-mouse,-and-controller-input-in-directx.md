---
title: Entrée d’un contrôleur dans DirectX, clavier et souris
description: Explique comment créer une application pour la réalité mixte Windows qui utilise des contrôleurs de jeu, clavier et souris.
author: MikeRiches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, clavier, souris, contrôleur de jeu, manette xbox, HoloLens, bureau, procédure pas à pas, exemple de code
ms.openlocfilehash: 1e61cb50a561492fdc6849b5b231e97fab1bb6cf
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597120"
---
# <a name="keyboard-mouse-and-controller-input-in-directx"></a><span data-ttu-id="3771f-104">Entrée d’un contrôleur dans DirectX, clavier et souris</span><span class="sxs-lookup"><span data-stu-id="3771f-104">Keyboard, mouse, and controller input in DirectX</span></span>

<span data-ttu-id="3771f-105">Claviers, souris et contrôleurs de jeu peuvent tous être des formulaires utiles d’entrée pour les appareils Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="3771f-105">Keyboards, mice, and game controllers can all be useful forms of input for Windows Mixed Reality devices.</span></span> <span data-ttu-id="3771f-106">Souris et claviers sont tous deux pris en charge sur HoloLens, pour une utilisation avec le débogage de votre application ou en tant qu’une autre forme d’entrée.</span><span class="sxs-lookup"><span data-stu-id="3771f-106">Bluetooth keyboards and mice are both supported on HoloLens, for use with debugging your app or as an alternate form of input.</span></span> <span data-ttu-id="3771f-107">Réalité mixte Windows prend également en charge des casques IMMERSIFS PC - où souris, les claviers et les contrôleurs de jeu historiquement, étaient la norme.</span><span class="sxs-lookup"><span data-stu-id="3771f-107">Windows Mixed Reality also supports immersive headsets attached to PCs - where mice, keyboards, and game controllers have historically been the norm.</span></span>

<span data-ttu-id="3771f-108">Pour utiliser l’entrée au clavier sur HoloLens, paire un clavier Bluetooth sur votre appareil ou entrée virtuelle via le Windows Device Portal.</span><span class="sxs-lookup"><span data-stu-id="3771f-108">To use keyboard input on HoloLens, pair a Bluetooth keyboard to your device or use virtual input via the Windows Device Portal.</span></span> <span data-ttu-id="3771f-109">Pour utiliser l’entrée au clavier tout en portant un casque immersif Windows Mixed Reality, attribuer le focus d’entrée à la réalité mixte en les plaçant sur l’appareil ou à l’aide de la clé de Windows + la combinaison de touches Y.</span><span class="sxs-lookup"><span data-stu-id="3771f-109">To use keyboard input while wearing a Windows Mixed Reality immersive headset, assign input focus to mixed reality by putting on the device or using the Windows Key + Y keyboard combination.</span></span> <span data-ttu-id="3771f-110">N’oubliez pas que les applications destinées à HoloLens doivent fournir des fonctionnalités sans ces périphériques connectés.</span><span class="sxs-lookup"><span data-stu-id="3771f-110">Keep in mind that apps intended for HoloLens must provide functionality without these devices attached.</span></span>

>[!NOTE]
><span data-ttu-id="3771f-111">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="3771f-111">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="3771f-112">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="3771f-112">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="subscribe-for-corewindow-input-events"></a><span data-ttu-id="3771f-113">Vous abonner aux événements d’entrée CoreWindow</span><span class="sxs-lookup"><span data-stu-id="3771f-113">Subscribe for CoreWindow input events</span></span>

### <a name="keyboard-input"></a><span data-ttu-id="3771f-114">Saisie au clavier</span><span class="sxs-lookup"><span data-stu-id="3771f-114">Keyboard input</span></span>

<span data-ttu-id="3771f-115">Dans le modèle d’application Windows HOLOGRAPHIQUE, nous incluons un gestionnaire d’événements pour l’entrée au clavier comme n’importe quel autre application UWP.</span><span class="sxs-lookup"><span data-stu-id="3771f-115">In the Windows Holographic app template, we include an event handler for keyboard input just like any other UWP app.</span></span> <span data-ttu-id="3771f-116">Votre application consomme les données d’entrée de clavier de la même manière dans Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="3771f-116">Your app consumes keyboard input data the same way in Windows Mixed Reality.</span></span>

<span data-ttu-id="3771f-117">À partir de AppView.cpp :</span><span class="sxs-lookup"><span data-stu-id="3771f-117">From AppView.cpp:</span></span>

```
// Register for keypress notifications.
   window->KeyDown +=
       ref new TypedEventHandler<CoreWindow^, KeyEventArgs^>(this, &AppView::OnKeyPressed);

    …

   // Input event handlers

   void AppView::OnKeyPressed(CoreWindow^ sender, KeyEventArgs^ args)
   {
       //
       // TODO: Respond to keyboard input here.
       //
   }
```

### <a name="virtual-keyboard-input"></a><span data-ttu-id="3771f-118">Entrée au clavier virtuel</span><span class="sxs-lookup"><span data-stu-id="3771f-118">Virtual keyboard input</span></span>
<span data-ttu-id="3771f-119">Pour des casques IMMERSIFS de bureau, vous pouvez prennent également en charge virtuels claviers restitués par Windows sur votre vue immersive.</span><span class="sxs-lookup"><span data-stu-id="3771f-119">For immersive desktop headsets, you can also support virtual keyboards rendered by Windows over your immersive view.</span></span> <span data-ttu-id="3771f-120">Pour ce faire, votre application peut implémenter **CoreTextEditContext**.</span><span class="sxs-lookup"><span data-stu-id="3771f-120">To support this, your app can implement **CoreTextEditContext**.</span></span> <span data-ttu-id="3771f-121">Cela permet de comprendre l’état de votre propre application rendu des zones de texte, donc le clavier virtuel peut correctement contribuer à l’il de texte Windows.</span><span class="sxs-lookup"><span data-stu-id="3771f-121">This lets Windows understand the state of your own app-rendered text boxes, so the virtual keyboard can correctly contribute to the text there.</span></span>

<span data-ttu-id="3771f-122">Pour plus d’informations sur l’implémentation de prise en charge CoreTextEditContext, consultez le [CoreTextEditContext exemple](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomEditControl).</span><span class="sxs-lookup"><span data-stu-id="3771f-122">For more information on implementing CoreTextEditContext support, see the [CoreTextEditContext sample](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomEditControl).</span></span>

### <a name="mouse-input"></a><span data-ttu-id="3771f-123">Entrée de la souris</span><span class="sxs-lookup"><span data-stu-id="3771f-123">Mouse Input</span></span>

<span data-ttu-id="3771f-124">Vous pouvez également utiliser les entrées de la souris, à nouveau par le biais de gestionnaires d’événements d’entrée UWP CoreWindow.</span><span class="sxs-lookup"><span data-stu-id="3771f-124">You can also use mouse input, again via the UWP CoreWindow input event handlers.</span></span> <span data-ttu-id="3771f-125">Voici comment modifier le modèle d’application Windows HOLOGRAPHIQUE pour prendre en charge les clics de souris dans les mouvements de façon aussi appuyés mêmes.</span><span class="sxs-lookup"><span data-stu-id="3771f-125">Here's how to modify the Windows Holographic app template to support mouse clicks in the same way as pressed gestures.</span></span> <span data-ttu-id="3771f-126">Après avoir effectué cette modification, un clic de souris tout en portant un appareil casque immersives se replacera le cube.</span><span class="sxs-lookup"><span data-stu-id="3771f-126">After making this modification, a mouse click while wearing an immersive headset device will reposition the cube.</span></span>

<span data-ttu-id="3771f-127">Notez que les applications UWP peuvent également obtenir des données XY brutes la souris à l’aide de la [MouseDevice](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.MouseDevice) API.</span><span class="sxs-lookup"><span data-stu-id="3771f-127">Note that UWP apps can also get raw XY data for the mouse by using the [MouseDevice](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.MouseDevice) API.</span></span>

<span data-ttu-id="3771f-128">Commencez par déclarer un nouveau gestionnaire OnPointerPressed dans AppView.h :</span><span class="sxs-lookup"><span data-stu-id="3771f-128">Start by declaring a new OnPointerPressed handler in AppView.h:</span></span>

```
protected:
       void OnPointerPressed(Windows::UI::Core::CoreWindow^ sender, Windows::UI::Core::PointerEventArgs^ args);
```

<span data-ttu-id="3771f-129">Dans AppView.cpp, ajoutez ce code à SetWindow :</span><span class="sxs-lookup"><span data-stu-id="3771f-129">In AppView.cpp, add this code to SetWindow:</span></span>

```
// Register for pointer pressed notifications.
   window->PointerPressed +=
       ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &AppView::OnPointerPressed);
```

<span data-ttu-id="3771f-130">Puis, placez cette définition pour OnPointerPressed en bas du fichier :</span><span class="sxs-lookup"><span data-stu-id="3771f-130">Then put this definition for OnPointerPressed at the bottom of the file:</span></span>

```
void AppView::OnPointerPressed(CoreWindow^ sender, PointerEventArgs^ args)
   {
       // Allow the user to interact with the holographic world using the mouse.
       if (m_main != nullptr)
       {
           m_main->OnPointerPressed();
       }
   }
```

<span data-ttu-id="3771f-131">Nous venons d’ajouter le Gestionnaire d’événements est un transfert à la classe de modèle principal.</span><span class="sxs-lookup"><span data-stu-id="3771f-131">The event handler we just added is a pass-through to the template main class.</span></span> <span data-ttu-id="3771f-132">Nous allons modifier la classe principale pour prendre en charge cette transmission.</span><span class="sxs-lookup"><span data-stu-id="3771f-132">Let's modify the main class to support this pass-through.</span></span> <span data-ttu-id="3771f-133">Ajoutez cette déclaration de méthode publique pour le fichier d’en-tête :</span><span class="sxs-lookup"><span data-stu-id="3771f-133">Add this public method declaration to the header file:</span></span>

```
// Handle mouse input.
       void OnPointerPressed();
```

<span data-ttu-id="3771f-134">Vous aurez besoin de cette variable de membre privé :</span><span class="sxs-lookup"><span data-stu-id="3771f-134">You'll need this private member variable, as well:</span></span>

```
// Keep track of mouse input.
       bool m_pointerPressed = false;
```

<span data-ttu-id="3771f-135">Enfin, nous mettrons à jour la classe principale avec la nouvelle logique pour prendre en charge les clics de souris.</span><span class="sxs-lookup"><span data-stu-id="3771f-135">Finally, we will update the main class with new logic to support mouse clicks.</span></span> <span data-ttu-id="3771f-136">Commencez par ajouter ce gestionnaire d’événements.</span><span class="sxs-lookup"><span data-stu-id="3771f-136">Start by adding this event handler.</span></span> <span data-ttu-id="3771f-137">Veillez à mettre à jour le nom de classe :</span><span class="sxs-lookup"><span data-stu-id="3771f-137">Make sure to update the class name:</span></span>

```
void MyHolographicAppMain::OnPointerPressed()
   {
       m_pointerPressed = true;
   }
```

<span data-ttu-id="3771f-138">Maintenant, dans la méthode de mise à jour, remplacer la logique existante pour obtenir une pose de pointeur avec ceci :</span><span class="sxs-lookup"><span data-stu-id="3771f-138">Now, in the Update method, replace the existing logic for getting a pointer pose with this:</span></span>

```
SpatialInteractionSourceState^ pointerState = m_spatialInputHandler->CheckForInput();
   SpatialPointerPose^ pose = nullptr;
   if (pointerState != nullptr)
   {
       pose = pointerState->TryGetPointerPose(currentCoordinateSystem);
   }
   else if (m_pointerPressed)
   {
       pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
   }
   m_pointerPressed = false;
```

<span data-ttu-id="3771f-139">Recompilez et redéployez.</span><span class="sxs-lookup"><span data-stu-id="3771f-139">Recompile and redeploy.</span></span> <span data-ttu-id="3771f-140">Vous devriez remarquer que le clic de souris se replacera maintenant le cube dans votre casque immersif - ou le HoloLens avec la souris bluetooth attachée.</span><span class="sxs-lookup"><span data-stu-id="3771f-140">You should notice that the mouse click will now reposition the cube in your immersive headset - or HoloLens with bluetooth mouse attached.</span></span>

### <a name="game-controller-support"></a><span data-ttu-id="3771f-141">Prise en charge du contrôleur de jeu</span><span class="sxs-lookup"><span data-stu-id="3771f-141">Game controller support</span></span>

<span data-ttu-id="3771f-142">Contrôleurs de jeu peuvent être un cadre amusant et un moyen pratique de permettre à l’utilisateur de contrôler une expérience d’immersion Windows Mixed Reality.</span><span class="sxs-lookup"><span data-stu-id="3771f-142">Game controllers can be a fun and convenient way of allowing the user to control an immersive Windows Mixed Reality experience.</span></span>

<span data-ttu-id="3771f-143">La première étape lors de l’ajout de prise en charge des contrôleurs de jeu pour le modèle d’application Windows HOLOGRAPHIQUE consiste à ajouter les déclarations de membre privé suivantes à la classe de l’en-tête de votre fichier principal :</span><span class="sxs-lookup"><span data-stu-id="3771f-143">The first step in adding support for game controllers to the Windows Holographic app template, is to add the following private member declarations to the header class for your main file:</span></span>

```
// Recognize gamepads that are plugged in after the app starts.
       void OnGamepadAdded(Platform::Object^, Windows::Gaming::Input::Gamepad^ args);
```

```
// Stop looking for gamepads that are unplugged.
       void OnGamepadRemoved(Platform::Object^, Windows::Gaming::Input::Gamepad^ args);
```

```
Windows::Foundation::EventRegistrationToken                     m_gamepadAddedEventToken;
       Windows::Foundation::EventRegistrationToken                     m_gamepadRemovedEventToken;
```

```
// Keeps track of a gamepad and the state of its A button.
       struct GamepadWithButtonState
       {
           Windows::Gaming::Input::Gamepad^ gamepad;
           bool buttonAWasPressedLastFrame = false;
       };
       std::vector<GamepadWithButtonState>                             m_gamepads;
```

<span data-ttu-id="3771f-144">Initialiser les événements gamepad et les boîtiers de commande associées, dans le constructeur de votre classe principale :</span><span class="sxs-lookup"><span data-stu-id="3771f-144">Initialize gamepad events, and any gamepads that are currently attached, in the constructor for your main class:</span></span>

```
// If connected, a game controller can also be used for input.
   m_gamepadAddedEventToken = Gamepad::GamepadAdded +=
       ref new EventHandler<Gamepad^>(
           bind(&$safeprojectname$Main::OnGamepadAdded, this, _1, _2)
           );
```

```
m_gamepadRemovedEventToken = Gamepad::GamepadRemoved +=
       ref new EventHandler<Gamepad^>(
           bind(&$safeprojectname$Main::OnGamepadRemoved, this, _1, _2)
           );
```

```
for (auto const& gamepad : Gamepad::Gamepads)
   {
       OnGamepadAdded(nullptr, gamepad);
   }
```

<span data-ttu-id="3771f-145">Ajoutez ces gestionnaires d’événements à votre classe principale.</span><span class="sxs-lookup"><span data-stu-id="3771f-145">Add these event handlers to your main class.</span></span> <span data-ttu-id="3771f-146">Veillez à mettre à jour le nom de classe :</span><span class="sxs-lookup"><span data-stu-id="3771f-146">Make sure to update the class name:</span></span>

```
void MyHolographicAppMain::OnGamepadAdded(Object^, Gamepad^ args)
   {
       for (auto const& gamepadWithButtonState : m_gamepads)
       {
           if (args == gamepadWithButtonState.gamepad)
           {
               // This gamepad is already in the list.
               return;
           }
       }
       m_gamepads.push_back({ args, false });
   }
```

```
void MyHolographicAppMain::OnGamepadRemoved(Object^, Gamepad^ args)
   {
       m_gamepads.erase(
           std::remove_if(m_gamepads.begin(), m_gamepads.end(), [&](GamepadWithButtonState& gamepadWithState)
               {
                   return gamepadWithState.gamepad == args;
               }),
           m_gamepads.end());
   }
```

<span data-ttu-id="3771f-147">Enfin, mettez à jour la logique d’entrée afin qu’il reconnaisse les modifications de l’état du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="3771f-147">Finally, update the input logic to recognize changes in controller state.</span></span> <span data-ttu-id="3771f-148">Ici, nous utilisons la même variable m_pointerPressed décrite dans la section ci-dessus pour l’ajout d’événements de souris.</span><span class="sxs-lookup"><span data-stu-id="3771f-148">Here, we use the same m_pointerPressed variable discussed in the section above for adding mouse events.</span></span> <span data-ttu-id="3771f-149">Ajoutez ceci à la méthode de mise à jour, juste avant où il vérifie le SpatialPointerPose :</span><span class="sxs-lookup"><span data-stu-id="3771f-149">Add this to the Update method, just before where it checks for the SpatialPointerPose:</span></span>

```
// Check for new input state since the last frame.
   for (auto& gamepadWithButtonState : m_gamepads)
   {
       bool buttonDownThisUpdate = ((gamepadWithButtonState.gamepad->GetCurrentReading().Buttons & GamepadButtons::A) == GamepadButtons::A);
       if (buttonDownThisUpdate && !gamepadWithButtonState.buttonAWasPressedLastFrame)
       {
           m_pointerPressed = true;
       }
       gamepadWithButtonState.buttonAWasPressedLastFrame = buttonDownThisUpdate;
   }
```

```
// For context.
   SpatialInteractionSourceState^ pointerState = m_spatialInputHandler->CheckForInput();
   SpatialPointerPose^ pose = nullptr;
   if (pointerState != nullptr)
   {
       pose = pointerState->TryGetPointerPose(currentCoordinateSystem);
   }
   else if (m_pointerPressed)
   {
       pose = SpatialPointerPose::TryGetAtTimestamp(currentCoordinateSystem, prediction->Timestamp);
   }
   m_pointerPressed = false;
```

<span data-ttu-id="3771f-150">N’oubliez pas d’annuler l’inscription des événements lors du nettoyage de la classe principale :</span><span class="sxs-lookup"><span data-stu-id="3771f-150">Don't forget to unregister the events when cleaning up the main class:</span></span>

```
if (m_gamepadAddedEventToken.Value != 0)
   {
       Gamepad::GamepadAdded -= m_gamepadAddedEventToken;
   }
   if (m_gamepadRemovedEventToken.Value != 0)
   {
       Gamepad::GamepadRemoved -= m_gamepadRemovedEventToken;
   }
```

<span data-ttu-id="3771f-151">Recompilez et redéployez.</span><span class="sxs-lookup"><span data-stu-id="3771f-151">Recompile, and redeploy.</span></span> <span data-ttu-id="3771f-152">Vous pouvez désormais joindre, ou paire, un contrôleur de jeu et utilisez-le pour repositionner le cube en rotation.</span><span class="sxs-lookup"><span data-stu-id="3771f-152">You can now attach, or pair, a game controller and use it to reposition the spinning cube.</span></span>

## <a name="important-guidelines-for-keyboard-and-mouse-input"></a><span data-ttu-id="3771f-153">Instructions importantes pour l’entrée clavier et souris</span><span class="sxs-lookup"><span data-stu-id="3771f-153">Important guidelines for keyboard and mouse input</span></span>

<span data-ttu-id="3771f-154">Il existe quelques différences importantes dans la façon dont ce code peut être utilisé sur Microsoft HoloLens – qui est un périphérique qui s’appuie principalement sur une entrée utilisateur naturelle – par rapport à ce qui est disponible sur un PC Windows Mixed Reality-activé.</span><span class="sxs-lookup"><span data-stu-id="3771f-154">There are some key differences in how this code can be used on Microsoft HoloLens – which is a device that relies primarily on natural user input – versus what is available on a Windows Mixed Reality-enabled PC.</span></span>
* <span data-ttu-id="3771f-155">Vous ne pouvez pas compter sur le clavier ou de la souris à être présent.</span><span class="sxs-lookup"><span data-stu-id="3771f-155">You can’t rely on keyboard or mouse input to be present.</span></span> <span data-ttu-id="3771f-156">Toutes les fonctionnalités de votre application doivent utiliser des regards, mouvement et la saisie vocale.</span><span class="sxs-lookup"><span data-stu-id="3771f-156">All of your app's functionality must work with gaze, gesture, and speech input.</span></span>
* <span data-ttu-id="3771f-157">Lorsqu’un clavier Bluetooth est attaché, il peut être utile d’activer l’entrée au clavier pour n’importe quel texte qui peut demander votre application.</span><span class="sxs-lookup"><span data-stu-id="3771f-157">When a Bluetooth keyboard is attached, it can be helpful to enable keyboard input for any text that your app might ask for.</span></span> <span data-ttu-id="3771f-158">Cela peut être un excellent supplément de dictée, par exemple.</span><span class="sxs-lookup"><span data-stu-id="3771f-158">This can be a great supplement for dictation, for example.</span></span>
* <span data-ttu-id="3771f-159">Lorsqu’il s’agit de conception de votre application, ne vous fiez WASD (par exemple) et la souris rechercher des contrôles à votre jeu.</span><span class="sxs-lookup"><span data-stu-id="3771f-159">When it comes to designing your app, don’t rely on (for example) WASD and mouse look controls for your game.</span></span> <span data-ttu-id="3771f-160">HoloLens est conçu pour l’utilisateur à parcourir autour de la pièce.</span><span class="sxs-lookup"><span data-stu-id="3771f-160">HoloLens is designed for the user to walk around the room.</span></span> <span data-ttu-id="3771f-161">Dans ce cas, l’utilisateur contrôle directement l’appareil photo.</span><span class="sxs-lookup"><span data-stu-id="3771f-161">In this case, the user controls the camera directly.</span></span> <span data-ttu-id="3771f-162">Une interface de commande de l’appareil photo autour de la pièce avec des contrôles de déplacement/aspect ne fournit la même expérience.</span><span class="sxs-lookup"><span data-stu-id="3771f-162">An interface for driving the camera around the room with move/look controls won't provide the same experience.</span></span>
* <span data-ttu-id="3771f-163">Entrée au clavier peut être un excellent moyen de contrôler les aspects de débogage de votre application ou le moteur de jeu, en particulier parce que l’utilisateur ne sera pas nécessaire pour utiliser le clavier.</span><span class="sxs-lookup"><span data-stu-id="3771f-163">Keyboard input can be an excellent way to control the debugging aspects of your app or game engine, especially since the user will not be required to use the keyboard.</span></span> <span data-ttu-id="3771f-164">Mettre en place des est le même que vous êtes habitué, avec les API d’événements CoreWindow.</span><span class="sxs-lookup"><span data-stu-id="3771f-164">Wiring it up is the same as you're used to, with CoreWindow event APIs.</span></span> <span data-ttu-id="3771f-165">Dans ce scénario, vous pouvez choisir d’implémenter une méthode pour configurer votre application pour acheminer les événements de clavier à un mode « debug entrée uniquement » au cours de vos sessions de débogage.</span><span class="sxs-lookup"><span data-stu-id="3771f-165">In this scenario, you might choose to implement a way to configure your app to route keyboard events to a "debug input only" mode during your debug sessions.</span></span>
* <span data-ttu-id="3771f-166">Les contrôleurs Bluetooth fonctionnent également.</span><span class="sxs-lookup"><span data-stu-id="3771f-166">Bluetooth controllers work as well.</span></span>

## <a name="see-also"></a><span data-ttu-id="3771f-167">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3771f-167">See also</span></span>
* [<span data-ttu-id="3771f-168">Accessoires de matériel</span><span class="sxs-lookup"><span data-stu-id="3771f-168">Hardware accessories</span></span>](hardware-accessories.md)
