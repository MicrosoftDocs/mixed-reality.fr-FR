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
# <a name="keyboard-input-in-unity"></a><span data-ttu-id="3507a-104">Entrée au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="3507a-104">Keyboard input in Unity</span></span>

<span data-ttu-id="3507a-105">**Espace de noms :** *UnityEngine*</span><span class="sxs-lookup"><span data-stu-id="3507a-105">**Namespace:** *UnityEngine*</span></span><br>
 <span data-ttu-id="3507a-106">**Type**:  *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span><span class="sxs-lookup"><span data-stu-id="3507a-106">**Type**: *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span></span>

<span data-ttu-id="3507a-107">Alors que HoloLens prend en charge de nombreuses formes d’entrée, y compris les claviers Bluetooth, la plupart des applications ne peuvent pas supposer que tous les utilisateurs disposent d’un clavier physique disponible.</span><span class="sxs-lookup"><span data-stu-id="3507a-107">While HoloLens supports many forms of input including Bluetooth keyboards, most applications cannot assume that all users will have a physical keyboard available.</span></span> <span data-ttu-id="3507a-108">Si votre application nécessite une entrée de texte, une forme de clavier à l’écran doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="3507a-108">If your application requires text input, some form of on screen keyboard should be provided.</span></span>

<span data-ttu-id="3507a-109">Unity fournit la classe *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="3507a-109">Unity provides the *[TouchScreenKeyboard](https://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* class for accepting keyboard input when there is no physical keyboard available.</span></span>

## <a name="hololens-system-keyboard-behavior-in-unity"></a><span data-ttu-id="3507a-110">Comportement du clavier du système HoloLens dans Unity</span><span class="sxs-lookup"><span data-stu-id="3507a-110">HoloLens system keyboard behavior in Unity</span></span>

<span data-ttu-id="3507a-111">Sur HoloLens, *TouchScreenKeyboard* utilise le clavier du système sur l’écran.</span><span class="sxs-lookup"><span data-stu-id="3507a-111">On HoloLens, the *TouchScreenKeyboard* leverages the system's on screen keyboard.</span></span> <span data-ttu-id="3507a-112">Le clavier sur l’écran du système ne peut pas se superposer au-dessus d’une vue volumétrique. ainsi, Unity doit créer une vue XAML 2D secondaire pour afficher le clavier, puis revenir à la vue volumétrique une fois que l’entrée a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="3507a-112">The system's on screen keyboard is unable to overlay on top of a volumetric view so Unity has to create a secondary 2D XAML view to show the keyboard then return back to the volumetric view once input has been submitted.</span></span> <span data-ttu-id="3507a-113">Le workflow utilisateur se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="3507a-113">The user flow goes like this:</span></span>
1. <span data-ttu-id="3507a-114">L’utilisateur effectue une action provoquant l’appel du code d’application *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="3507a-114">The user performs an action causing app code to call *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="3507a-115">L’application est responsable de la suspension de l’état de l’application avant d’appeler *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="3507a-115">The app is responsible for pausing app state before calling *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="3507a-116">L’application peut se terminer avant de revenir à la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="3507a-116">The app may terminate before ever switching back to the volumetric view</span></span>
2. <span data-ttu-id="3507a-117">Unity bascule vers une vue XAML 2D qui est placée automatiquement dans le monde</span><span class="sxs-lookup"><span data-stu-id="3507a-117">Unity switches to a 2D XAML view which is auto-placed in the world</span></span>
3. <span data-ttu-id="3507a-118">L’utilisateur entre du texte à l’aide du clavier du système et envoie ou annule</span><span class="sxs-lookup"><span data-stu-id="3507a-118">The user enters text using the system keyboard and submits or cancels</span></span>
4. <span data-ttu-id="3507a-119">Le commutateur Unity revient à la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="3507a-119">Unity switches back to the volumetric view</span></span>
    * <span data-ttu-id="3507a-120">L’application est responsable de la reprise de l’état de l’application lorsque le *TouchScreenKeyboard* est terminé</span><span class="sxs-lookup"><span data-stu-id="3507a-120">The app is responsible for resuming app state when the *TouchScreenKeyboard* is done</span></span>
5. <span data-ttu-id="3507a-121">Le texte envoyé est disponible dans le *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="3507a-121">Submitted text is available in the *TouchScreenKeyboard*</span></span>

### <a name="available-keyboard-views"></a><span data-ttu-id="3507a-122">Affichages du clavier disponibles</span><span class="sxs-lookup"><span data-stu-id="3507a-122">Available keyboard views</span></span>

<span data-ttu-id="3507a-123">Six différentes vues du clavier sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="3507a-123">There are six different keyboard views available:</span></span>
* <span data-ttu-id="3507a-124">Zone de texte sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="3507a-124">Single-line textbox</span></span>
* <span data-ttu-id="3507a-125">Zone de texte sur une seule ligne avec titre</span><span class="sxs-lookup"><span data-stu-id="3507a-125">Single-line textbox with title</span></span>
* <span data-ttu-id="3507a-126">Zone de texte multiligne</span><span class="sxs-lookup"><span data-stu-id="3507a-126">Multi-line textbox</span></span>
* <span data-ttu-id="3507a-127">Zone de texte multiligne avec titre</span><span class="sxs-lookup"><span data-stu-id="3507a-127">Multi-line textbox with title</span></span>
* <span data-ttu-id="3507a-128">Zone de mot de passe sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="3507a-128">Single-line password box</span></span>
* <span data-ttu-id="3507a-129">Zone de mot de passe sur une seule ligne avec titre</span><span class="sxs-lookup"><span data-stu-id="3507a-129">Single-line password box with title</span></span>

## <a name="how-to-enable-the-system-keyboard-in-unity"></a><span data-ttu-id="3507a-130">Comment activer le clavier système dans Unity</span><span class="sxs-lookup"><span data-stu-id="3507a-130">How to enable the system keyboard in Unity</span></span>

<span data-ttu-id="3507a-131">Le clavier du système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le « type de build UWP » défini sur « XAML ».</span><span class="sxs-lookup"><span data-stu-id="3507a-131">The HoloLens system keyboard is only available to Unity applications that are exported with the "UWP Build Type" set to "XAML".</span></span> <span data-ttu-id="3507a-132">Vous effectuez des compromis lorsque vous choisissez « XAML » comme « type de build UWP » sur « D3D ».</span><span class="sxs-lookup"><span data-stu-id="3507a-132">There are tradeoffs you make when you choose "XAML" as the "UWP Build Type" over "D3D".</span></span> <span data-ttu-id="3507a-133">Si vous n’êtes pas familiarisé avec ces compromis, vous souhaiterez peut-être explorer une [solution d’entrée alternative](#alternative-keyboard-options) au clavier du système.</span><span class="sxs-lookup"><span data-stu-id="3507a-133">If you aren't comfortable with those tradeoffs, you may wish to explore an [alternative input solution](#alternative-keyboard-options) to the system keyboard.</span></span>
1. <span data-ttu-id="3507a-134">Ouvrez le menu **fichier** et sélectionnez **paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="3507a-134">Open the **File** menu and select **Build Settings...**</span></span>
2. <span data-ttu-id="3507a-135">Assurez-vous que la **plateforme** est définie sur **Windows Store**, que le **Kit de développement logiciel (SDK)** est défini sur **Universal 10**et que vous définissez le **type de build UWP** sur **XAML**.</span><span class="sxs-lookup"><span data-stu-id="3507a-135">Ensure the **Platform** is set to **Windows Store**, the **SDK** is set to **Universal 10**, and set the **UWP Build Type** to **XAML**.</span></span>
3. <span data-ttu-id="3507a-136">Dans la boîte de dialogue **paramètres de build** , cliquez sur le bouton **paramètres du lecteur..** .</span><span class="sxs-lookup"><span data-stu-id="3507a-136">In the **Build Settings** dialog, click the **Player Settings...** button</span></span>
4. <span data-ttu-id="3507a-137">Select the **Settings for Windows Store** tab</span><span class="sxs-lookup"><span data-stu-id="3507a-137">Select the **Settings for Windows Store** tab</span></span>
5. <span data-ttu-id="3507a-138">Expand the **Other Settings** group</span><span class="sxs-lookup"><span data-stu-id="3507a-138">Expand the **Other Settings** group</span></span>
6. <span data-ttu-id="3507a-139">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality Devices** list</span><span class="sxs-lookup"><span data-stu-id="3507a-139">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality Devices** list</span></span>
7. <span data-ttu-id="3507a-140">Ensure **Windows Holographic** appears in the list of Virtual Reality SDKs</span><span class="sxs-lookup"><span data-stu-id="3507a-140">Ensure **Windows Holographic** appears in the list of Virtual Reality SDKs</span></span>

>[!NOTE]
><span data-ttu-id="3507a-141">If you don't mark the build as Virtual Reality Supported with the HoloLens device, the project will export as a 2D XAML app.</span><span class="sxs-lookup"><span data-stu-id="3507a-141">If you don't mark the build as Virtual Reality Supported with the HoloLens device, the project will export as a 2D XAML app.</span></span>

## <a name="using-the-system-keyboard-in-your-unity-app"></a><span data-ttu-id="3507a-142">Using the system keyboard in your Unity app</span><span class="sxs-lookup"><span data-stu-id="3507a-142">Using the system keyboard in your Unity app</span></span>

### <a name="declare-the-keyboard"></a><span data-ttu-id="3507a-143">Declare the keyboard</span><span class="sxs-lookup"><span data-stu-id="3507a-143">Declare the keyboard</span></span>

<span data-ttu-id="3507a-144">In the class, declare a variable to store the *TouchScreenKeyboard* and a variable to hold the string the keyboard returns.</span><span class="sxs-lookup"><span data-stu-id="3507a-144">In the class, declare a variable to store the *TouchScreenKeyboard* and a variable to hold the string the keyboard returns.</span></span>

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a><span data-ttu-id="3507a-145">Invoke the keyboard</span><span class="sxs-lookup"><span data-stu-id="3507a-145">Invoke the keyboard</span></span>

<span data-ttu-id="3507a-146">When an event occurs requesting keyboard input, call one of these functions depending upon the type of input desired.</span><span class="sxs-lookup"><span data-stu-id="3507a-146">When an event occurs requesting keyboard input, call one of these functions depending upon the type of input desired.</span></span> <span data-ttu-id="3507a-147">Note that the title is specified in the textPlaceholder parameter.</span><span class="sxs-lookup"><span data-stu-id="3507a-147">Note that the title is specified in the textPlaceholder parameter.</span></span>

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

### <a name="retrieve-typed-contents"></a><span data-ttu-id="3507a-148">Retrieve typed contents</span><span class="sxs-lookup"><span data-stu-id="3507a-148">Retrieve typed contents</span></span>

<span data-ttu-id="3507a-149">In the update loop, check if the keyboard received new input and store it for use elsewhere.</span><span class="sxs-lookup"><span data-stu-id="3507a-149">In the update loop, check if the keyboard received new input and store it for use elsewhere.</span></span>

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

## <a name="alternative-keyboard-options"></a><span data-ttu-id="3507a-150">Alternative keyboard options</span><span class="sxs-lookup"><span data-stu-id="3507a-150">Alternative keyboard options</span></span>

<span data-ttu-id="3507a-151">We understand that switching out of a volumetric view into a 2D view isn't the ideal way to get text input from the user.</span><span class="sxs-lookup"><span data-stu-id="3507a-151">We understand that switching out of a volumetric view into a 2D view isn't the ideal way to get text input from the user.</span></span>

<span data-ttu-id="3507a-152">The current alternatives to leveraging the system keyboard through Unity include:</span><span class="sxs-lookup"><span data-stu-id="3507a-152">The current alternatives to leveraging the system keyboard through Unity include:</span></span>
* <span data-ttu-id="3507a-153">Using speech dictation for input (<b>Note:</b> this is often error prone for words not found in the dictionary and is not suitable for password entry)</span><span class="sxs-lookup"><span data-stu-id="3507a-153">Using speech dictation for input (<b>Note:</b> this is often error prone for words not found in the dictionary and is not suitable for password entry)</span></span>
* <span data-ttu-id="3507a-154">Create a keyboard that works in your applications exclusive view</span><span class="sxs-lookup"><span data-stu-id="3507a-154">Create a keyboard that works in your applications exclusive view</span></span>
