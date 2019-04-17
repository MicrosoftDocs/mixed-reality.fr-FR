---
title: Entrée au clavier dans Unity
description: Unity fournit la classe TouchScreenKeyboard pour accepter une entrée de clavier lorsqu’il n’existe pas de clavier physique disponible.
author: thetuvix
ms.author: alexturn
ms.date: 03/21/2018
ms.topic: article
keywords: unity d’entrée, clavier, touchscreenkeyboard
ms.openlocfilehash: 35f6f0df993931eea35db7b167110b341ea0c0f2
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59597040"
---
# <a name="keyboard-input-in-unity"></a><span data-ttu-id="af0a5-104">Entrée au clavier dans Unity</span><span class="sxs-lookup"><span data-stu-id="af0a5-104">Keyboard input in Unity</span></span>

<span data-ttu-id="af0a5-105">**Namespace :** *UnityEngine*</span><span class="sxs-lookup"><span data-stu-id="af0a5-105">**Namespace:** *UnityEngine*</span></span><br>
 <span data-ttu-id="af0a5-106">**Type** : *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span><span class="sxs-lookup"><span data-stu-id="af0a5-106">**Type**: *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)*</span></span>

<span data-ttu-id="af0a5-107">HoloLens prend en charge de nombreux formulaires d’entrée, y compris les claviers, la plupart des applications ne peut pas supposer que tous les utilisateurs auront un clavier physique disponible.</span><span class="sxs-lookup"><span data-stu-id="af0a5-107">While HoloLens supports many forms of input including Bluetooth keyboards, most applications cannot assume that all users will have a physical keyboard available.</span></span> <span data-ttu-id="af0a5-108">Si votre application nécessite la saisie de texte, une forme de clavier de l’écran doit être fournie.</span><span class="sxs-lookup"><span data-stu-id="af0a5-108">If your application requires text input, some form of on screen keyboard should be provided.</span></span>

<span data-ttu-id="af0a5-109">Unity fournit le *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* classe permettant d’accepter l’entrée au clavier lorsqu’il n’existe pas de clavier physique disponible.</span><span class="sxs-lookup"><span data-stu-id="af0a5-109">Unity provides the *[TouchScreenKeyboard](http://docs.unity3d.com/ScriptReference/TouchScreenKeyboard.html)* class for accepting keyboard input when there is no physical keyboard available.</span></span>

## <a name="hololens-system-keyboard-behavior-in-unity"></a><span data-ttu-id="af0a5-110">Comportement du clavier système HoloLens dans Unity</span><span class="sxs-lookup"><span data-stu-id="af0a5-110">HoloLens system keyboard behavior in Unity</span></span>

<span data-ttu-id="af0a5-111">Sur HoloLens, le *TouchScreenKeyboard* se sert du système sur le clavier de l’écran.</span><span class="sxs-lookup"><span data-stu-id="af0a5-111">On HoloLens, the *TouchScreenKeyboard* leverages the system's on screen keyboard.</span></span> <span data-ttu-id="af0a5-112">Le système sur le clavier visuel est incapable de superposer sur une vue volumétrique Unity doit donc créer une vue XAML 2D secondaire pour afficher le clavier puis à revenir dans la vue volumétrique une fois que l’entrée a été envoyée.</span><span class="sxs-lookup"><span data-stu-id="af0a5-112">The system's on screen keyboard is unable to overlay on top of a volumetric view so Unity has to create a secondary 2D XAML view to show the keyboard then return back to the volumetric view once input has been submitted.</span></span> <span data-ttu-id="af0a5-113">Le flux de l’utilisateur se déroule comme suit :</span><span class="sxs-lookup"><span data-stu-id="af0a5-113">The user flow goes like this:</span></span>
1. <span data-ttu-id="af0a5-114">L’utilisateur effectue une action à l’origine du code d’application pour appeler *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="af0a5-114">The user performs an action causing app code to call *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="af0a5-115">L’application est responsable de l’état de mise en pause l’application avant d’appeler *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="af0a5-115">The app is responsible for pausing app state before calling *TouchScreenKeyboard*</span></span>
    * <span data-ttu-id="af0a5-116">L’application peut se fermer avant de basculer jamais revenir à la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="af0a5-116">The app may terminate before ever switching back to the volumetric view</span></span>
2. <span data-ttu-id="af0a5-117">Unity bascule vers une vue XAML 2D qui est placés automatiquement dans le monde</span><span class="sxs-lookup"><span data-stu-id="af0a5-117">Unity switches to a 2D XAML view which is auto-placed in the world</span></span>
3. <span data-ttu-id="af0a5-118">L’utilisateur entre du texte à l’aide du clavier système et soumet ou annule</span><span class="sxs-lookup"><span data-stu-id="af0a5-118">The user enters text using the system keyboard and submits or cancels</span></span>
4. <span data-ttu-id="af0a5-119">Unity bascule vers la vue volumétrique</span><span class="sxs-lookup"><span data-stu-id="af0a5-119">Unity switches back to the volumetric view</span></span>
    * <span data-ttu-id="af0a5-120">L’application est responsable de l’application de reprise état lorsque le *TouchScreenKeyboard* est effectuée</span><span class="sxs-lookup"><span data-stu-id="af0a5-120">The app is responsible for resuming app state when the *TouchScreenKeyboard* is done</span></span>
5. <span data-ttu-id="af0a5-121">Texte soumis est disponible dans le *TouchScreenKeyboard*</span><span class="sxs-lookup"><span data-stu-id="af0a5-121">Submitted text is available in the *TouchScreenKeyboard*</span></span>

### <a name="available-keyboard-views"></a><span data-ttu-id="af0a5-122">Vues de clavier disponibles</span><span class="sxs-lookup"><span data-stu-id="af0a5-122">Available keyboard views</span></span>

<span data-ttu-id="af0a5-123">Il existe six clavier différentes vues disponibles :</span><span class="sxs-lookup"><span data-stu-id="af0a5-123">There are six different keyboard views available:</span></span>
* <span data-ttu-id="af0a5-124">Zone de texte monoligne</span><span class="sxs-lookup"><span data-stu-id="af0a5-124">Single-line textbox</span></span>
* <span data-ttu-id="af0a5-125">Zone de texte monoligne avec titre</span><span class="sxs-lookup"><span data-stu-id="af0a5-125">Single-line textbox with title</span></span>
* <span data-ttu-id="af0a5-126">Zone de texte multiligne</span><span class="sxs-lookup"><span data-stu-id="af0a5-126">Multi-line textbox</span></span>
* <span data-ttu-id="af0a5-127">Zone de texte multiligne avec titre</span><span class="sxs-lookup"><span data-stu-id="af0a5-127">Multi-line textbox with title</span></span>
* <span data-ttu-id="af0a5-128">Zone de mot de passe une ligne</span><span class="sxs-lookup"><span data-stu-id="af0a5-128">Single-line password box</span></span>
* <span data-ttu-id="af0a5-129">Zone de mot de passe une ligne avec titre</span><span class="sxs-lookup"><span data-stu-id="af0a5-129">Single-line password box with title</span></span>

## <a name="how-to-enable-the-system-keyboard-in-unity"></a><span data-ttu-id="af0a5-130">Comment activer le clavier système dans Unity</span><span class="sxs-lookup"><span data-stu-id="af0a5-130">How to enable the system keyboard in Unity</span></span>

<span data-ttu-id="af0a5-131">Le clavier système HoloLens est uniquement disponible pour les applications Unity qui sont exportées avec le « UWP Build Type » défini sur « XAML ».</span><span class="sxs-lookup"><span data-stu-id="af0a5-131">The HoloLens system keyboard is only available to Unity applications that are exported with the "UWP Build Type" set to "XAML".</span></span> <span data-ttu-id="af0a5-132">Il existe des compromis que vous effectuez lorsque vous choisissez « XAML » comme le « Type de Build UWP » sur « D3D ».</span><span class="sxs-lookup"><span data-stu-id="af0a5-132">There are tradeoffs you make when you choose "XAML" as the "UWP Build Type" over "D3D".</span></span> <span data-ttu-id="af0a5-133">Si vous n’êtes pas familiarisé avec ces compromis, vous pouvez Explorer une [solution d’entrée de remplacement](#alternative-keyboard-options) au clavier système.</span><span class="sxs-lookup"><span data-stu-id="af0a5-133">If you aren't comfortable with those tradeoffs, you may wish to explore an [alternative input solution](#alternative-keyboard-options) to the system keyboard.</span></span>
1. <span data-ttu-id="af0a5-134">Ouvrez le **fichier** menu et sélectionnez **paramètres de Build...**</span><span class="sxs-lookup"><span data-stu-id="af0a5-134">Open the **File** menu and select **Build Settings...**</span></span>
2. <span data-ttu-id="af0a5-135">Garantir la **plateforme** a la valeur **Windows Store**, le **SDK** a la valeur **universelle 10**et définissez la **Type de Build UWP**  à **XAML**.</span><span class="sxs-lookup"><span data-stu-id="af0a5-135">Ensure the **Platform** is set to **Windows Store**, the **SDK** is set to **Universal 10**, and set the **UWP Build Type** to **XAML**.</span></span>
3. <span data-ttu-id="af0a5-136">Dans le **paramètres de Build** boîte de dialogue, cliquez sur le **paramètres du lecteur...**  bouton</span><span class="sxs-lookup"><span data-stu-id="af0a5-136">In the **Build Settings** dialog, click the **Player Settings...** button</span></span>
4. <span data-ttu-id="af0a5-137">Sélectionnez le **paramètres pour Windows Store** onglet</span><span class="sxs-lookup"><span data-stu-id="af0a5-137">Select the **Settings for Windows Store** tab</span></span>
5. <span data-ttu-id="af0a5-138">Développez le **autres paramètres** groupe</span><span class="sxs-lookup"><span data-stu-id="af0a5-138">Expand the **Other Settings** group</span></span>
6. <span data-ttu-id="af0a5-139">Dans le **rendu** section, vérifiez le **virtuel pris en charge de réalité** case à cocher pour ajouter un nouveau **des appareils de réalité virtuelle** liste</span><span class="sxs-lookup"><span data-stu-id="af0a5-139">In the **Rendering** section, check the **Virtual Reality Supported** checkbox to add a new **Virtual Reality Devices** list</span></span>
7. <span data-ttu-id="af0a5-140">Vérifiez **Windows HOLOGRAPHIQUE** s’affiche dans la liste des kits SDK de réalité virtuelle</span><span class="sxs-lookup"><span data-stu-id="af0a5-140">Ensure **Windows Holographic** appears in the list of Virtual Reality SDKs</span></span>

>[!NOTE]
><span data-ttu-id="af0a5-141">Si vous ne marquez pas la build en tant que la prise en charge du réalité virtuelle avec l’appareil HoloLens, le projet sera exporter en tant qu’une application XAML 2D.</span><span class="sxs-lookup"><span data-stu-id="af0a5-141">If you don't mark the build as Virtual Reality Supported with the HoloLens device, the project will export as a 2D XAML app.</span></span>

## <a name="using-the-system-keyboard-in-your-unity-app"></a><span data-ttu-id="af0a5-142">À l’aide du clavier système dans votre application Unity</span><span class="sxs-lookup"><span data-stu-id="af0a5-142">Using the system keyboard in your Unity app</span></span>

### <a name="declare-the-keyboard"></a><span data-ttu-id="af0a5-143">Déclarez le clavier</span><span class="sxs-lookup"><span data-stu-id="af0a5-143">Declare the keyboard</span></span>

<span data-ttu-id="af0a5-144">Dans la classe, déclarez une variable pour stocker le *TouchScreenKeyboard* et retourne une variable pour contenir la chaîne à l’aide du clavier.</span><span class="sxs-lookup"><span data-stu-id="af0a5-144">In the class, declare a variable to store the *TouchScreenKeyboard* and a variable to hold the string the keyboard returns.</span></span>

```cs
UnityEngine.TouchScreenKeyboard keyboard;
public static string keyboardText = "";
```

### <a name="invoke-the-keyboard"></a><span data-ttu-id="af0a5-145">Appeler le clavier</span><span class="sxs-lookup"><span data-stu-id="af0a5-145">Invoke the keyboard</span></span>

<span data-ttu-id="af0a5-146">Lorsqu’un événement survient demandeur entrée au clavier, appelez une de ces fonctions selon le type d’entrée que vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="af0a5-146">When an event occurs requesting keyboard input, call one of these functions depending upon the type of input desired.</span></span> <span data-ttu-id="af0a5-147">Notez que le titre est spécifié dans le paramètre textPlaceholder.</span><span class="sxs-lookup"><span data-stu-id="af0a5-147">Note that the title is specified in the textPlaceholder parameter.</span></span>

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

### <a name="retrieve-typed-contents"></a><span data-ttu-id="af0a5-148">Récupérer le contenu typé</span><span class="sxs-lookup"><span data-stu-id="af0a5-148">Retrieve typed contents</span></span>

<span data-ttu-id="af0a5-149">Dans la boucle de mise à jour, vérifiez si le clavier a reçu une nouvelle entrée et stockez-le pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="af0a5-149">In the update loop, check if the keyboard received new input and store it for use elsewhere.</span></span>

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

## <a name="alternative-keyboard-options"></a><span data-ttu-id="af0a5-150">Options de remplacement de clavier</span><span class="sxs-lookup"><span data-stu-id="af0a5-150">Alternative keyboard options</span></span>

<span data-ttu-id="af0a5-151">Nous sommes conscients que hors d’une vue volumétrique dans une vue en 2D de commutation n’est pas le moyen idéal pour obtenir une entrée de texte à partir de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="af0a5-151">We understand that switching out of a volumetric view into a 2D view isn't the ideal way to get text input from the user.</span></span>

<span data-ttu-id="af0a5-152">Les alternatives actuels pour exploiter le clavier système via Unity incluent :</span><span class="sxs-lookup"><span data-stu-id="af0a5-152">The current alternatives to leveraging the system keyboard through Unity include:</span></span>
* <span data-ttu-id="af0a5-153">À l’aide de la dictée vocale pour l’entrée (<b>Remarque :</b> cela est souvent sujette aux erreurs dans introuvable dans le dictionnaire de mots et ne convient pas pour l’entrée de mot de passe)</span><span class="sxs-lookup"><span data-stu-id="af0a5-153">Using speech dictation for input (<b>Note:</b> this is often error prone for words not found in the dictionary and is not suitable for password entry)</span></span>
* <span data-ttu-id="af0a5-154">Créer un clavier fonctionne dans votre vue exclusif des applications</span><span class="sxs-lookup"><span data-stu-id="af0a5-154">Create a keyboard that works in your applications exclusive view</span></span>
