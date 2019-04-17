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
# <a name="keyboard-mouse-and-controller-input-in-directx"></a>Entrée d’un contrôleur dans DirectX, clavier et souris

Claviers, souris et contrôleurs de jeu peuvent tous être des formulaires utiles d’entrée pour les appareils Windows Mixed Reality. Souris et claviers sont tous deux pris en charge sur HoloLens, pour une utilisation avec le débogage de votre application ou en tant qu’une autre forme d’entrée. Réalité mixte Windows prend également en charge des casques IMMERSIFS PC - où souris, les claviers et les contrôleurs de jeu historiquement, étaient la norme.

Pour utiliser l’entrée au clavier sur HoloLens, paire un clavier Bluetooth sur votre appareil ou entrée virtuelle via le Windows Device Portal. Pour utiliser l’entrée au clavier tout en portant un casque immersif Windows Mixed Reality, attribuer le focus d’entrée à la réalité mixte en les plaçant sur l’appareil ou à l’aide de la clé de Windows + la combinaison de touches Y. N’oubliez pas que les applications destinées à HoloLens doivent fournir des fonctionnalités sans ces périphériques connectés.

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

## <a name="subscribe-for-corewindow-input-events"></a>Vous abonner aux événements d’entrée CoreWindow

### <a name="keyboard-input"></a>Saisie au clavier

Dans le modèle d’application Windows HOLOGRAPHIQUE, nous incluons un gestionnaire d’événements pour l’entrée au clavier comme n’importe quel autre application UWP. Votre application consomme les données d’entrée de clavier de la même manière dans Windows Mixed Reality.

À partir de AppView.cpp :

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

### <a name="virtual-keyboard-input"></a>Entrée au clavier virtuel
Pour des casques IMMERSIFS de bureau, vous pouvez prennent également en charge virtuels claviers restitués par Windows sur votre vue immersive. Pour ce faire, votre application peut implémenter **CoreTextEditContext**. Cela permet de comprendre l’état de votre propre application rendu des zones de texte, donc le clavier virtuel peut correctement contribuer à l’il de texte Windows.

Pour plus d’informations sur l’implémentation de prise en charge CoreTextEditContext, consultez le [CoreTextEditContext exemple](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomEditControl).

### <a name="mouse-input"></a>Entrée de la souris

Vous pouvez également utiliser les entrées de la souris, à nouveau par le biais de gestionnaires d’événements d’entrée UWP CoreWindow. Voici comment modifier le modèle d’application Windows HOLOGRAPHIQUE pour prendre en charge les clics de souris dans les mouvements de façon aussi appuyés mêmes. Après avoir effectué cette modification, un clic de souris tout en portant un appareil casque immersives se replacera le cube.

Notez que les applications UWP peuvent également obtenir des données XY brutes la souris à l’aide de la [MouseDevice](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.MouseDevice) API.

Commencez par déclarer un nouveau gestionnaire OnPointerPressed dans AppView.h :

```
protected:
       void OnPointerPressed(Windows::UI::Core::CoreWindow^ sender, Windows::UI::Core::PointerEventArgs^ args);
```

Dans AppView.cpp, ajoutez ce code à SetWindow :

```
// Register for pointer pressed notifications.
   window->PointerPressed +=
       ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &AppView::OnPointerPressed);
```

Puis, placez cette définition pour OnPointerPressed en bas du fichier :

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

Nous venons d’ajouter le Gestionnaire d’événements est un transfert à la classe de modèle principal. Nous allons modifier la classe principale pour prendre en charge cette transmission. Ajoutez cette déclaration de méthode publique pour le fichier d’en-tête :

```
// Handle mouse input.
       void OnPointerPressed();
```

Vous aurez besoin de cette variable de membre privé :

```
// Keep track of mouse input.
       bool m_pointerPressed = false;
```

Enfin, nous mettrons à jour la classe principale avec la nouvelle logique pour prendre en charge les clics de souris. Commencez par ajouter ce gestionnaire d’événements. Veillez à mettre à jour le nom de classe :

```
void MyHolographicAppMain::OnPointerPressed()
   {
       m_pointerPressed = true;
   }
```

Maintenant, dans la méthode de mise à jour, remplacer la logique existante pour obtenir une pose de pointeur avec ceci :

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

Recompilez et redéployez. Vous devriez remarquer que le clic de souris se replacera maintenant le cube dans votre casque immersif - ou le HoloLens avec la souris bluetooth attachée.

### <a name="game-controller-support"></a>Prise en charge du contrôleur de jeu

Contrôleurs de jeu peuvent être un cadre amusant et un moyen pratique de permettre à l’utilisateur de contrôler une expérience d’immersion Windows Mixed Reality.

La première étape lors de l’ajout de prise en charge des contrôleurs de jeu pour le modèle d’application Windows HOLOGRAPHIQUE consiste à ajouter les déclarations de membre privé suivantes à la classe de l’en-tête de votre fichier principal :

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

Initialiser les événements gamepad et les boîtiers de commande associées, dans le constructeur de votre classe principale :

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

Ajoutez ces gestionnaires d’événements à votre classe principale. Veillez à mettre à jour le nom de classe :

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

Enfin, mettez à jour la logique d’entrée afin qu’il reconnaisse les modifications de l’état du contrôleur. Ici, nous utilisons la même variable m_pointerPressed décrite dans la section ci-dessus pour l’ajout d’événements de souris. Ajoutez ceci à la méthode de mise à jour, juste avant où il vérifie le SpatialPointerPose :

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

N’oubliez pas d’annuler l’inscription des événements lors du nettoyage de la classe principale :

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

Recompilez et redéployez. Vous pouvez désormais joindre, ou paire, un contrôleur de jeu et utilisez-le pour repositionner le cube en rotation.

## <a name="important-guidelines-for-keyboard-and-mouse-input"></a>Instructions importantes pour l’entrée clavier et souris

Il existe quelques différences importantes dans la façon dont ce code peut être utilisé sur Microsoft HoloLens – qui est un périphérique qui s’appuie principalement sur une entrée utilisateur naturelle – par rapport à ce qui est disponible sur un PC Windows Mixed Reality-activé.
* Vous ne pouvez pas compter sur le clavier ou de la souris à être présent. Toutes les fonctionnalités de votre application doivent utiliser des regards, mouvement et la saisie vocale.
* Lorsqu’un clavier Bluetooth est attaché, il peut être utile d’activer l’entrée au clavier pour n’importe quel texte qui peut demander votre application. Cela peut être un excellent supplément de dictée, par exemple.
* Lorsqu’il s’agit de conception de votre application, ne vous fiez WASD (par exemple) et la souris rechercher des contrôles à votre jeu. HoloLens est conçu pour l’utilisateur à parcourir autour de la pièce. Dans ce cas, l’utilisateur contrôle directement l’appareil photo. Une interface de commande de l’appareil photo autour de la pièce avec des contrôles de déplacement/aspect ne fournit la même expérience.
* Entrée au clavier peut être un excellent moyen de contrôler les aspects de débogage de votre application ou le moteur de jeu, en particulier parce que l’utilisateur ne sera pas nécessaire pour utiliser le clavier. Mettre en place des est le même que vous êtes habitué, avec les API d’événements CoreWindow. Dans ce scénario, vous pouvez choisir d’implémenter une méthode pour configurer votre application pour acheminer les événements de clavier à un mode « debug entrée uniquement » au cours de vos sessions de débogage.
* Les contrôleurs Bluetooth fonctionnent également.

## <a name="see-also"></a>Voir aussi
* [Accessoires de matériel](hardware-accessories.md)
