---
title: Entrée au clavier dans Unity
description: Unity fournit la classe TouchScreenKeyboard pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: clavier, entrée, Unity, touchscreenkeyboard
ms.openlocfilehash: 35f6f0df993931eea35db7b167110b341ea0c0f2
ms.sourcegitcommit: 915d3cc63a5571ba22ac4608589f3eca8da1bc81
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/24/2019
ms.locfileid: "63515737"
---
# <a name="keyboard-input-in-unity"></a><span data-ttu-id="ffea7-104">Entrée au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="ffea7-104">Keyboard input in Unity</span></span>

<span data-ttu-id="ffea7-105">**Espace de noms :** *UnityEngine*</span><span class="sxs-lookup"><span data-stu-id="ffea7-105">**Namespace:** *UnityEngine*</span></span><br>
 <span data-ttu-id="ffea7-106">**Type** : *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span><span class="sxs-lookup"><span data-stu-id="ffea7-106">**Type**: *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span></span>

<span data-ttu-id="ffea7-107">Alors que HoloLens prend en charge de nombreuses formes d’entrée, y compris les claviers Bluetooth, la plupart des applications ne peuvent pas supposer que tous les utilisateurs disposent d’un clavier physique disponible.</span><span class="sxs-lookup"><span data-stu-id="ffea7-107">While HoloLens supports many forms of input including Bluetooth keyboards, most applications cannot assume that all users will have a physical keyboard available.</span></span> <span data-ttu-id="ffea7-108">Si votre application nécessite une entrée de texte, une forme de clavier à l’écran doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="ffea7-108">If your application requires text input, some form of on screen keyboard should be provided.</span></span>

<span data-ttu-id="ffea7-109">Unity fournit la classe *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* pour accepter l’entrée au clavier quand aucun clavier physique n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="ffea7-109">Unity provides the *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* class for accepting keyboard input when there is no physical keyboard available.</span></span>

## <a name="hololens-system-keyboard-behavior-in-unity"></a><span data-ttu-id="ffea7-110">Comportement du clavier du système HoloLens dans Unity</span><span class="sxs-lookup"><span data-stu-id="ffea7-110">HoloLens system keyboard behavior in Unity</span></span>

<span data-ttu-id="ffea7-111">Sur HoloLens, *TouchScreenKeyboard* utilise le clavier du système sur l’écran.</span><span class="sxs-lookup"><span data-stu-id="ffea7-111">On HoloLens, the *TouchScreenKeyboard* leverages the system's on screen keyboard.</span></span> <span data-ttu-id="ffea7-112">Le clavier sur l’écran du système ne peut pas se superposer au-dessus d’une vue volumétrique. ainsi, Unity doit créer une vue XAML 2D secondaire pour afficher le clavier, puis revenir à la vue volumétrique une fois que l’entrée a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="ffea7-112">The system's on screen keyboard is unable to overlay on top of a volumetric view so Unity has to create a secondary 2D XAML view to show the keyboard then return back to the volumetric view once input has been submitted.</span></span> <span data-ttu-id="ffea7-113">Le workflow utilisateur se présente comme suit:</span><span class="sxs-lookup"><span data-stu-id="ffea7-113">The user flow goes like this:</span></span>
1. <span data-ttu-id="ffea7-114">L’utilisateur effectue une action provoquant l’appel du code d’application *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="ffea7-114">The user performs an action causing app code to call *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="ffea7-115">L’application est responsable de la suspension de l’état de l’application avant d’appeler *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="ffea7-115">The app is responsible for pausing app state before calling *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="ffea7-116">L’application peut se terminer avant de revenir à la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="ffea7-116">The app may terminate before ever switching back to the volumetric view</span></span>
2. <span data-ttu-id="ffea7-117">Unity bascule vers une vue XAML 2D qui est placée automatiquement dans le monde</span><span class="sxs-lookup"><span data-stu-id="ffea7-117">Unity switches to a 2D XAML view which is auto-placed in the world</span></span>
3. <span data-ttu-id="ffea7-118">L’utilisateur entre du texte à l’aide du clavier du système et envoie ou annule</span><span class="sxs-lookup"><span data-stu-id="ffea7-118">The user enters text using the system keyboard and submits or cancels</span></span>
4. <span data-ttu-id="ffea7-119">Le commutateur Unity revient à la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="ffea7-119">Unity switches back to the volumetric view</span></span>
    * <span data-ttu-id="ffea7-120">L’application est responsable de la reprise de l’état de l’application lorsque le *TouchScreenKeyboard* est terminé</span><span class="sxs-lookup"><span data-stu-id="ffea7-120">The app is responsible for resuming app state when the *TouchScreenKeyboard* is done</span></span>
5. <span data-ttu-id="ffea7-121">Le texte envoyé est disponible dans le *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="ffea7-121">Submitted text is available in the *TouchScreenKeyboard*</span></span>

### <a name="available-keyboard-views"></a><span data-ttu-id="ffea7-122">Affichages du clavier disponibles</span><span class="sxs-lookup"><span data-stu-id="ffea7-122">Available keyboard views</span></span>

<span data-ttu-id="ffea7-123">Six différentes vues du clavier sont disponibles:</span><span class="sxs-lookup"><span data-stu-id="ffea7-123">There are six different keyboard views available:</span></span>
* <span data-ttu-id="ffea7-124">Zone de texte sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="ffea7-124">Single-line textbox</span></span>
* <span data-ttu-id="ffea7-125">Zone de texte sur une seule ligne avec titre</span><span class="sxs-lookup"><span data-stu-id="ffea7-125">Single-line textbox with title</span></span>
* <span data-ttu-id="ffea7-126">Zone de texte multiligne</span><span class="sxs-lookup"><span data-stu-id="ffea7-126">Multi-line textbox</span></span>
* <span data-ttu-id="ffea7-127">Zone de texte multiligne avec titre</span><span class="sxs-lookup"><span data-stu-id="ffea7-127">Multi-line textbox with title</span></span>
* <span data-ttu-id="ffea7-128">Zone de mot de passe sur une seule ligne</span><span class="sxs-lookup"><span data-stu-id="ffea7-128">Single-line password box</span></span>
* <span data-ttu-id="ffea7-129">Zone de mot de passe sur une seule ligne avec titre</span><span class="sxs-lookup"><span data-stu-id="ffea7-129">Single-line password box with title</span></span>

## <a name="how-to-enable-the-system-keyboard-in-unity"></a><span data-ttu-id="ffea7-130">Comment activer le clavier système dans Unity</span><span class="sxs-lookup"><span data-stu-id="ffea7-130">How to enable the system keyboard in Unity</span></span>

<span data-ttu-id="ffea7-131">Le clavier du système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le «type de build UWP» défini sur «XAML».</span><span class="sxs-lookup"><span data-stu-id="ffea7-131">The HoloLens system keyboard is only available to Unity applications that are exported with the "UWP Build Type" set to "XAML".</span></span> <span data-ttu-id="ffea7-132">Vous effectuez des compromis lorsque vous choisissez «XAML» comme «type de build UWP» sur «D3D».</span><span class="sxs-lookup"><span data-stu-id="ffea7-132">There are tradeoffs you make when you choose "XAML" as the "UWP Build Type" over "D3D".</span></span> <span data-ttu-id="ffea7-133">Si vous n’êtes pas familiarisé avec ces compromis, vous souhaiterez peut-être explorer une [solution d’entrée alternative](#alternative-keyboard-options) au clavier du système.</span><span class="sxs-lookup"><span data-stu-id="ffea7-133">If you aren't comfortable with those tradeoffs, you may wish to explore an [alternative input solution](#alternative-keyboard-options) to the system keyboard.</span></span>
1. <span data-ttu-id="ffea7-134">Ouvrez le menu **fichier** et sélectionnez **paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="ffea7-134">Open the **File** menu and select **Build Settings...**</span></span>
2. <span data-ttu-id="ffea7-135">Assurez-vous que la **plateforme** est définie sur **Windows Store**, que le **Kit de développement logiciel (SDK)** est défini sur **Universal 10**et que vous définissez le **type de build UWP** sur **XAML**.</span><span class="sxs-lookup"><span data-stu-id="ffea7-135">Ensure the **Platform** is set to **Windows Store**, the **SDK** is set to **Universal 10**, and set the **UWP Build Type** to **XAML**.</span></span>
3. <span data-ttu-id="ffea7-136">Dans la boîte de dialogue **paramètres de build** , cliquez sur le bouton **paramètres du lecteur..** .</span><span class="sxs-lookup"><span data-stu-id="ffea7-136">In the **Build Settings** dialog, click the **Player Settings...** button</span></span>
4. <span data-ttu-id="ffea7-137">Sélectionner les **paramètres pour l’onglet Windows Store**</span><span class="sxs-lookup"><span data-stu-id="ffea7-137">Select the **Settings for Windows Store** tab</span></span>
5. <span data-ttu-id="ffea7-138">Développer le groupe **autres paramètres**</span><span class="sxs-lookup"><span data-stu-id="ffea7-138">Expand the **Other Settings** group</span></span>
6. <span data-ttu-id="ffea7-139">Dans la section **rendu** , activez la case à cocher **réalité virtuelle prise en charge** pour ajouter une nouvelle liste d' **appareils de réalité virtuelle**</span><span class="sxs-lookup"><span data-stu-id="ffea7-139">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality Devices** list</span></span>
7. <span data-ttu-id="ffea7-140">S’assurer que **Windows holographique** apparaît dans la liste des kits de développement logiciel (SDK) de réalité virtuelle</span><span class="sxs-lookup"><span data-stu-id="ffea7-140">Ensure **Windows Holographic** appears in the list of Virtual Reality SDKs</span></span>

>[!NOTE]
><span data-ttu-id="ffea7-141">Si vous ne Marquez pas la build comme une réalité virtuelle prise en charge avec l’appareil HoloLens, le projet sera exporté en tant qu’application XAML 2D.</span><span class="sxs-lookup"><span data-stu-id="ffea7-141">If you don't mark the build as Virtual Reality Supported with the HoloLens device, the project will export as a 2D XAML app.</span></span>

## <a name="using-the-system-keyboard-in-your-unity-app"></a><span data-ttu-id="ffea7-142">Utilisation du clavier système dans votre application Unity</span><span class="sxs-lookup"><span data-stu-id="ffea7-142">Using the system keyboard in your Unity app</span></span>

### <a name="declare-the-keyboard"></a><span data-ttu-id="ffea7-143">Déclarer le clavier</span><span class="sxs-lookup"><span data-stu-id="ffea7-143">Declare the keyboard</span></span>

<span data-ttu-id="ffea7-144">Dans la classe, déclarez une variable pour stocker le *TouchScreenKeyboard* et une variable qui contiendra la chaîne retournée par le clavier.</span><span class="sxs-lookup"><span data-stu-id="ffea7-144">In the class, declare a variable to store the *TouchScreenKeyboard* and a variable to hold the string the keyboard returns.</span></span>

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a><span data-ttu-id="ffea7-145">Appeler le clavier</span><span class="sxs-lookup"><span data-stu-id="ffea7-145">Invoke the keyboard</span></span>

<span data-ttu-id="ffea7-146">Lorsqu’un événement se produit en demandant une entrée au clavier, appelez l’une de ces fonctions en fonction du type d’entrée souhaité.</span><span class="sxs-lookup"><span data-stu-id="ffea7-146">When an event occurs requesting keyboard input, call one of these functions depending upon the type of input desired.</span></span> <span data-ttu-id="ffea7-147">Notez que le titre est spécifié dans le paramètre textPlaceholder.</span><span class="sxs-lookup"><span data-stu-id="ffea7-147">Note that the title is specified in the textPlaceholder parameter.</span></span>

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

### <a name="retrieve-typed-contents"></a><span data-ttu-id="ffea7-148">Récupérer le contenu typé</span><span class="sxs-lookup"><span data-stu-id="ffea7-148">Retrieve typed contents</span></span>

<span data-ttu-id="ffea7-149">Dans la boucle de mise à jour, vérifiez si le clavier a reçu une nouvelle entrée et stockez-la pour l’utiliser ailleurs.</span><span class="sxs-lookup"><span data-stu-id="ffea7-149">In the update loop, check if the keyboard received new input and store it for use elsewhere.</span></span>

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

## <a name="alternative-keyboard-options"></a><span data-ttu-id="ffea7-150">Autres options de clavier</span><span class="sxs-lookup"><span data-stu-id="ffea7-150">Alternative keyboard options</span></span>

<span data-ttu-id="ffea7-151">Nous savons que le basculement d’une vue volumétrique dans une vue 2D n’est pas la méthode idéale pour obtenir une entrée de texte de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ffea7-151">We understand that switching out of a volumetric view into a 2D view isn't the ideal way to get text input from the user.</span></span>

<span data-ttu-id="ffea7-152">Les alternatives actuelles à l’utilisation du clavier système via Unity sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="ffea7-152">The current alternatives to leveraging the system keyboard through Unity include:</span></span>
* <span data-ttu-id="ffea7-153">Utilisation de la dictée vocale pour l’entrée (<b>Remarque:</b> cela est souvent sujet à des erreurs pour les mots introuvables dans le dictionnaire et ne convient pas pour une entrée de mot de passe)</span><span class="sxs-lookup"><span data-stu-id="ffea7-153">Using speech dictation for input (<b>Note:</b> this is often error prone for words not found in the dictionary and is not suitable for password entry)</span></span>
* <span data-ttu-id="ffea7-154">Créer un clavier qui fonctionne en mode exclusif dans vos applications</span><span class="sxs-lookup"><span data-stu-id="ffea7-154">Create a keyboard that works in your applications exclusive view</span></span>
