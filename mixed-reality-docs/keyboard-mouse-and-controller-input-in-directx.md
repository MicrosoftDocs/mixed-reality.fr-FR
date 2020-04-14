---
title: Entrée de clavier, de souris et de contrôleur dans DirectX
description: Explique comment créer une application pour Windows Mixed Reality qui utilise le clavier, la souris et les contrôleurs de jeu.
author: mikeriches
ms.author: mriches
ms.date: 03/21/2018
ms.topic: article
keywords: Windows Mixed Reality, clavier, souris, contrôleur de jeu, contrôleur Xbox, HoloLens, Desktop, procédure pas à pas, exemple de code
ms.openlocfilehash: 27f1bf72435ce6889ba3f7b83664367a4440b162
ms.sourcegitcommit: d6ac8f1f545fe20cf1e36b83c0e7998b82fd02f8
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81278087"
---
# <a name="keyboard-mouse-and-controller-input-in-directx"></a>Entrée de clavier, de souris et de contrôleur dans DirectX

Les claviers, les souris et les contrôleurs de jeu peuvent être des formes d’entrée utiles pour les appareils Windows Mixed Reality. Les claviers et souris Bluetooth sont pris en charge sur HoloLens, pour être utilisés avec le débogage de votre application ou comme une autre forme d’entrée. Windows Mixed Reality prend également en charge les casques immersifs attachés à des PC, où les souris, les claviers et les contrôleurs de jeu étaient traditionnellement la norme.

Pour utiliser l’entrée au clavier sur HoloLens, couplez un clavier Bluetooth à votre appareil ou utilisez une entrée virtuelle via le portail de périphériques Windows. Pour utiliser l’entrée au clavier tout en portant un casque immersif Windows Mixed Reality, affectez le focus d’entrée à la réalité mixte en plaçant sur l’appareil ou en utilisant la combinaison de touches Windows + Y. Gardez à l’esprit que les applications destinées à HoloLens doivent fournir des fonctionnalités sans que ces appareils soient attachés.

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="subscribe-for-corewindow-input-events"></a>S’abonner aux événements d’entrée CoreWindow

### <a name="keyboard-input"></a>Saisie au clavier

Dans le modèle d’application holographique Windows, nous incluons un gestionnaire d’événements pour l’entrée au clavier comme n’importe quelle autre application UWP. Votre application utilise les données d’entrée au clavier de la même façon dans Windows Mixed Reality.

À partir de AppView. cpp :

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
Pour les casques de bureau immersifs, vous pouvez également prendre en charge des claviers virtuels rendus par Windows sur votre vue immersif. Pour prendre cela en charge, votre application peut implémenter **CoreTextEditContext**. Cela permet à Windows de comprendre l’état de vos propres zones de texte de rendu d’application, de sorte que le clavier virtuel puisse contribuer correctement au texte.

Pour plus d’informations sur l’implémentation de la prise en charge de CoreTextEditContext, consultez l' [exemple CoreTextEditContext](https://github.com/Microsoft/Windows-universal-samples/tree/master/Samples/CustomEditControl).

### <a name="mouse-input"></a>Entrée de la souris

Vous pouvez également utiliser l’entrée de la souris, à nouveau via les gestionnaires d’événements d’entrée UWP CoreWindow. Voici comment modifier le modèle d’application holographique Windows pour prendre en charge les clics de souris de la même façon que les gestes appuyés. Une fois cette modification effectuée, un clic de souris tout en faisant passer un périphérique de casque immersif repositionne le cube.

Notez que les applications UWP peuvent également obtenir des données brutes XY pour la souris à l’aide de l’API [MouseDevice](https://docs.microsoft.com/uwp/api/Windows.Devices.Input.MouseDevice) .

Commencez par déclarer un nouveau gestionnaire OnPointerPressed dans AppView. h :

```
protected:
       void OnPointerPressed(Windows::UI::Core::CoreWindow^ sender, Windows::UI::Core::PointerEventArgs^ args);
```

Dans AppView. cpp, ajoutez ce code à SetWindow :

```
// Register for pointer pressed notifications.
   window->PointerPressed +=
       ref new TypedEventHandler<CoreWindow^, PointerEventArgs^>(this, &AppView::OnPointerPressed);
```

Placez ensuite cette définition pour OnPointerPressed en bas du fichier :

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

Le gestionnaire d’événements que nous venons d’ajouter est un transfert vers la classe principale du modèle. Modifions la classe principale pour prendre en charge ce transfert. Ajoutez cette déclaration de méthode publique au fichier d’en-tête :

```
// Handle mouse input.
       void OnPointerPressed();
```

Vous aurez également besoin de cette variable de membre privé :

```
// Keep track of mouse input.
       bool m_pointerPressed = false;
```

Enfin, nous mettrons à jour la classe principale avec la nouvelle logique pour prendre en charge les clics de souris. Commencez par ajouter ce gestionnaire d’événements. Veillez à mettre à jour le nom de la classe :

```
void MyHolographicAppMain::OnPointerPressed()
   {
       m_pointerPressed = true;
   }
```

Maintenant, dans la méthode de mise à jour, remplacez la logique existante pour obtenir un pointeur à l’aide de ce qui suit :

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

Recompilez et redéployez. Notez que le clic de souris va à présent repositionner le cube dans votre casque immersif ou HoloLens avec la souris Bluetooth associée.

### <a name="game-controller-support"></a>Prise en charge des contrôleurs de jeu

Les contrôleurs de jeu peuvent être un moyen amusant et pratique de permettre à l’utilisateur de contrôler une expérience Windows Mixed Reality.

La première étape de l’ajout de la prise en charge des contrôleurs de jeu au modèle d’application holographique Windows consiste à ajouter les déclarations de membre privées suivantes à la classe d’en-tête de votre fichier principal :

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

Initialisez les événements de manette de main et tous les boîtiers de connexion actuellement attachés dans le constructeur de votre classe principale :

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

Ajoutez ces gestionnaires d’événements à votre classe principale. Veillez à mettre à jour le nom de la classe :

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

Enfin, mettez à jour la logique d’entrée pour reconnaître les modifications de l’état du contrôleur. Ici, nous utilisons la même m_pointerPressed variable traitée dans la section ci-dessus pour ajouter des événements de souris. Ajoutez-la à la méthode Update, juste avant l’emplacement où elle recherche le SpatialPointerPose :

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

Recompilez et redéployez. Vous pouvez maintenant attacher un contrôleur de jeu, ou le coupler, et l’utiliser pour repositionner le cube en rotation.

## <a name="important-guidelines-for-keyboard-and-mouse-input"></a>Indications importantes pour l’entrée au clavier et à la souris

Il existe quelques différences clés dans la façon dont ce code peut être utilisé sur Microsoft HoloLens, qui est un appareil qui s’appuie principalement sur l’entrée d’utilisateur naturelle, par rapport à ce qui est disponible sur un PC Windows Mixed Reality.
* Vous ne pouvez pas vous appuyer sur l’entrée du clavier ou de la souris. Toutes les fonctionnalités de votre application doivent fonctionner avec le regard, le geste et l’entrée vocale.
* Lorsqu’un clavier Bluetooth est attaché, il peut être utile d’activer l’entrée au clavier pour tout texte que votre application peut demander. Il peut s’agir d’un excellent complément pour la dictée, par exemple.
* Lorsqu’il s’agit de concevoir votre application, ne vous fiez pas (par exemple) aux contrôles WASD et Mouse pour votre jeu. HoloLens est conçu pour permettre à l’utilisateur de parcourir la salle. Dans ce cas, l’utilisateur contrôle directement l’appareil photo. Une interface pour la conduite de l’appareil photo autour de la salle avec des contrôles de déplacement/d’apparence n’offre pas la même expérience.
* L’entrée au clavier peut être un excellent moyen de contrôler les aspects de débogage de votre application ou moteur de jeu, en particulier dans la mesure où l’utilisateur ne sera pas obligé d’utiliser le clavier. Son câblage est identique à celui que vous utilisez avec les API d’événement CoreWindow. Dans ce scénario, vous pouvez choisir d’implémenter un moyen de configurer votre application pour acheminer les événements de clavier vers un mode « en entrée de débogage uniquement » pendant vos sessions de débogage.
* Les contrôleurs Bluetooth fonctionnent également.

## <a name="see-also"></a>Voir aussi
* [Accessoires matériels](hardware-accessories.md)
