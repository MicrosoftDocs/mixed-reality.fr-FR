---
title: Entrée au clavier dans Unity
description: Unity fournit la classe TouchScreenKeyboard pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: clavier, entrée, Unity, touchscreenkeyboard
ms.openlocfilehash: f506415f9658d9723bf31b339d63fe4569100ace
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73438552"
---
# <a name="keyboard-input-in-unity"></a>Entrée au clavier dans Unity

**Espace de noms :** *UnityEngine*<br>
 **Type**:  *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*

Alors que HoloLens prend en charge de nombreuses formes d’entrée, y compris les claviers Bluetooth, la plupart des applications ne peuvent pas supposer que tous les utilisateurs disposent d’un clavier physique disponible. Si votre application nécessite une entrée de texte, une forme de clavier à l’écran doit être fournie.

Unity fournit la classe *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.

## <a name="hololens-system-keyboard-behavior-in-unity"></a>Comportement du clavier du système HoloLens dans Unity

Sur HoloLens, *TouchScreenKeyboard* utilise le clavier du système sur l’écran. Le clavier sur l’écran du système ne peut pas se superposer au-dessus d’une vue volumétrique. ainsi, Unity doit créer une vue XAML 2D secondaire pour afficher le clavier, puis revenir à la vue volumétrique une fois que l’entrée a été envoyée. Le workflow utilisateur se présente comme suit :
1. L’utilisateur effectue une action provoquant l’appel du code d’application *TouchScreenKeyboard*
    * L’application est responsable de la suspension de l’état de l’application avant d’appeler *TouchScreenKeyboard*
    * L’application peut se terminer avant de revenir à la vue volumétrique
2. Unity bascule vers une vue XAML 2D qui est placée automatiquement dans le monde
3. L’utilisateur entre du texte à l’aide du clavier du système et envoie ou annule
4. Le commutateur Unity revient à la vue volumétrique
    * L’application est responsable de la reprise de l’état de l’application lorsque le *TouchScreenKeyboard* est terminé
5. Le texte envoyé est disponible dans le *TouchScreenKeyboard*

### <a name="available-keyboard-views"></a>Affichages du clavier disponibles

Six différentes vues du clavier sont disponibles :
* Zone de texte sur une seule ligne
* Zone de texte sur une seule ligne avec titre
* Zone de texte multiligne
* Zone de texte multiligne avec titre
* Zone de mot de passe sur une seule ligne
* Zone de mot de passe sur une seule ligne avec titre

## <a name="how-to-enable-the-system-keyboard-in-unity"></a>Comment activer le clavier système dans Unity

Le clavier du système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le « type de build UWP » défini sur « XAML ». Vous effectuez des compromis lorsque vous choisissez « XAML » comme « type de build UWP » sur « D3D ». Si vous n’êtes pas familiarisé avec ces compromis, vous souhaiterez peut-être explorer une [solution d’entrée alternative](#alternative-keyboard-options) au clavier du système.
1. Ouvrez le menu **fichier** et sélectionnez **paramètres de Build...**
2. Assurez-vous que la **plateforme** est définie sur **Windows Store**, que le **Kit de développement logiciel (SDK)** est défini sur **Universal 10**et que vous définissez le **type de build UWP** sur **XAML**.
3. Dans la boîte de dialogue **paramètres de build** , cliquez sur le bouton **paramètres du lecteur..** .
4. Select the **Settings for Windows Store** tab
5. Expand the **Other Settings** group
6. In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality Devices** list
7. Ensure **Windows Holographic** appears in the list of Virtual Reality SDKs

>[!NOTE]
>If you don't mark the build as Virtual Reality Supported with the HoloLens device, the project will export as a 2D XAML app.

## <a name="using-the-system-keyboard-in-your-unity-app"></a>Using the system keyboard in your Unity app

### <a name="declare-the-keyboard"></a>Declare the keyboard

In the class, declare a variable to store the *TouchScreenKeyboard* and a variable to hold the string the keyboard returns.

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a>Invoke the keyboard

When an event occurs requesting keyboard input, call one of these functions depending upon the type of input desired. Note that the title is specified in the textPlaceholder parameter.

```cs
// Single-line textbox
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, false, false);

// Single-line textbox with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, false, false, "Single-line title");

// Multi-line textbox
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, true, false, false);

// Multi-line textbox with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, true, false, false, "Multi-line Title");

// Single-line password box
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true, false);

// Single-line password box with title
keyboard = TouchScreenKeyboard.Open("", TouchScreenKeyboardType.Default, false, false, true, false, "Secure Single-line Title");
```

### <a name="retrieve-typed-contents"></a>Retrieve typed contents

In the update loop, check if the keyboard received new input and store it for use elsewhere.

```cs
if (TouchScreenKeyboard.visible == false && keyboard != null)
{
       if (keyboard.done == true)
       {
           keyboardText = keyboard.text;
           keyboard = null;
       }
}
```

## <a name="alternative-keyboard-options"></a>Alternative keyboard options

We understand that switching out of a volumetric view into a 2D view isn't the ideal way to get text input from the user.

The current alternatives to leveraging the system keyboard through Unity include:
* Using speech dictation for input (<b>Note:</b> this is often error prone for words not found in the dictionary and is not suitable for password entry)
* Create a keyboard that works in your applications exclusive view
