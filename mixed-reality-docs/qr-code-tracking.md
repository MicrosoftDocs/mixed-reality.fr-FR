---
title: Suivi du code QR
description: Apprenez à activer le suivi du code QR pour votre casque Windows Mixed Reality (VR) et implémentez la fonctionnalité dans vos applications VR.
author: yoyozilla
ms.author: yoyoz
ms.date: 11/06/2018
ms.topic: article
keywords: VR, LBE, divertissement basé sur l’emplacement, VR arcade, arcade, immersion, QR, code QR
ms.openlocfilehash: 465056cf645a8b9dc9e0e2d3f9dacf887df67c52
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829981"
---
# <a name="qr-code-tracking"></a><span data-ttu-id="b0cc7-104">Suivi du code QR</span><span class="sxs-lookup"><span data-stu-id="b0cc7-104">QR code tracking</span></span>

<span data-ttu-id="b0cc7-105">Le suivi du code QR est implémenté dans le pilote Windows Mixed Reality pour les casques immersif (VR).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-105">QR code tracking is implemented in the Windows Mixed Reality driver for immersive (VR) headsets.</span></span> <span data-ttu-id="b0cc7-106">En activant le dispositif de suivi du code QR dans le pilote du casque, le casque balaie les codes QR et ils sont signalés aux applications intéressées.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-106">By enabling the QR code tracker in the headset driver, the headset scans for QR codes and they are reported to interested apps.</span></span> <span data-ttu-id="b0cc7-107">Cette fonctionnalité est disponible uniquement à partir de la [mise à jour 2018 de Windows 10 octobre (également appelée RS5)](release-notes-october-2018.md).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-107">This feature is only available as of the [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md).</span></span>

>[!NOTE]
><span data-ttu-id="b0cc7-108">Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-108">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="b0cc7-109">Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-109">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="device-support"></a><span data-ttu-id="b0cc7-110">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="b0cc7-110">Device support</span></span>

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><span data-ttu-id="b0cc7-111"><strong>Fonctionnalité</strong></span><span class="sxs-lookup"><span data-stu-id="b0cc7-111"><strong>Feature</strong></span></span></td>
        <td><span data-ttu-id="b0cc7-112"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span><span class="sxs-lookup"><span data-stu-id="b0cc7-112"><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></span></span></td>
        <td><span data-ttu-id="b0cc7-113"><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></span><span class="sxs-lookup"><span data-stu-id="b0cc7-113"><a href="immersive-headset-hardware-details.md"><strong>Immersive headsets</strong></a></span></span></td>
    </tr>
     <tr>
        <td><span data-ttu-id="b0cc7-114">Suivi du code QR</span><span class="sxs-lookup"><span data-stu-id="b0cc7-114">QR code tracking</span></span></td>
        <td><span data-ttu-id="b0cc7-115">❌</span><span class="sxs-lookup"><span data-stu-id="b0cc7-115">❌</span></span></td>
        <td><span data-ttu-id="b0cc7-116">✔️</span><span class="sxs-lookup"><span data-stu-id="b0cc7-116">✔️</span></span></td>
    </tr>
</table>

## <a name="enabling-and-disabling-qr-code-tracking-for-your-headset"></a><span data-ttu-id="b0cc7-117">Activation et désactivation du suivi du code QR pour votre casque</span><span class="sxs-lookup"><span data-stu-id="b0cc7-117">Enabling and disabling QR code tracking for your headset</span></span>
<span data-ttu-id="b0cc7-118">Remarque : Cette section est uniquement valide pour la [mise à jour 2018 de Windows 10 octobre (également appelée RS5)](release-notes-october-2018.md).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-118">Note: This section is only valid for [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md).</span></span> <span data-ttu-id="b0cc7-119">À partir de 19h1 builds, vous n’aurez pas à le faire.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-119">From 19h1 builds onwards you will not have to do this.</span></span>
<span data-ttu-id="b0cc7-120">Que vous développiez une application de réalité mixte qui tire parti du suivi du code QR ou que vous soyez un client de l’une de ces applications, vous devez activer manuellement le suivi du code QR dans le pilote de votre casque.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-120">Whether you're developing a mixed reality app that will leverage QR code tracking, or you're a customer of one of these apps, you'll need to manually turn on QR code tracking in your headset's driver.</span></span>

<span data-ttu-id="b0cc7-121">Pour activer le **suivi du code QR** pour votre casque immersif:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-121">In order to **turn on QR code tracking** for your immersive (VR) headset:</span></span>

1. <span data-ttu-id="b0cc7-122">Fermez l’application portail de réalité mixte sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-122">Close the Mixed Reality Portal app on your PC.</span></span>
2. <span data-ttu-id="b0cc7-123">Débranchez le casque de votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-123">Unplug the headset from your PC.</span></span>
3. <span data-ttu-id="b0cc7-124">Exécutez le script suivant dans l’invite de commandes:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-124">Run the following script in the Command Prompt:</span></span><br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 1 /F`
4. <span data-ttu-id="b0cc7-125">Reconnectez votre casque à votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-125">Reconnect your headset to your PC.</span></span>

<span data-ttu-id="b0cc7-126">Pour désactiver le **suivi du code QR** pour votre casque immersif (VR):</span><span class="sxs-lookup"><span data-stu-id="b0cc7-126">In order to **turn off QR code tracking** for your immersive (VR) headset:</span></span>

1. <span data-ttu-id="b0cc7-127">Fermez l’application portail de réalité mixte sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-127">Close the Mixed Reality Portal app on your PC.</span></span>
2. <span data-ttu-id="b0cc7-128">Débranchez le casque de votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-128">Unplug the headset from your PC.</span></span>
3. <span data-ttu-id="b0cc7-129">Exécutez le script suivant dans l’invite de commandes:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-129">Run the following script in the Command Prompt:</span></span><br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 0 /F`
4. <span data-ttu-id="b0cc7-130">Reconnectez votre casque à votre PC.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-130">Reconnect your headset to your PC.</span></span> <span data-ttu-id="b0cc7-131">Cela rendra les codes QR détectés «non localisables».</span><span class="sxs-lookup"><span data-stu-id="b0cc7-131">This will make any discovered QR codes "non-locatable."</span></span>

## <a name="printing-codes"></a><span data-ttu-id="b0cc7-132">Codes d’impression</span><span class="sxs-lookup"><span data-stu-id="b0cc7-132">Printing codes</span></span>

<span data-ttu-id="b0cc7-133">Tout d’abord, la [spécification des codes QR](https://www.qrcode.com/en/howto/code.html) indique «la zone de symboles de code QR nécessite une marge ou une «zone calme» autour de celle-ci pour être utilisée.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-133">First and foremost, the [spec for QR codes](https://www.qrcode.com/en/howto/code.html) says "The QR Code symbol area requires a margin or "quiet zone" around it to be used.</span></span> <span data-ttu-id="b0cc7-134">La marge est une zone claire autour d’un symbole où rien n’est imprimé.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-134">The margin is a clear area around a symbol where nothing is printed.</span></span> <span data-ttu-id="b0cc7-135">Le code QR requiert une marge étendue à quatre modules sur tous les côtés d’un symbole.»</span><span class="sxs-lookup"><span data-stu-id="b0cc7-135">QR Code requires a four-module wide margin at all sides of a symbol."</span></span> <span data-ttu-id="b0cc7-136">Cela doit avoir une largeur, de chaque côté, de quatre fois la taille d’un module, un carré noir unique dans le code.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-136">This needs to have a width, on every side, of four times the size of a module - a single black square in the code.</span></span> <span data-ttu-id="b0cc7-137">La page spec contient des conseils sur la façon d’imprimer des codes QR et de déterminer la zone requise pour créer un code QR de taille spécifique.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-137">The spec page contains advice on how to print QR codes and figure out the area required to make a certain sized QR code.</span></span>

<span data-ttu-id="b0cc7-138">Actuellement, la qualité de la détection du code QR est susceptible de varier l’éclairage et le fond.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-138">Currently QR code detection quality is susceptible to varying illumination and backdrop.</span></span> <span data-ttu-id="b0cc7-139">Pour combattre cela, Notez votre éclairage et imprimez le code approprié.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-139">To combat this, note your illumination and print the appropriate code.</span></span> <span data-ttu-id="b0cc7-140">Dans une scène avec un éclairage particulièrement clair, imprimez un code noir sur un arrière-plan gris.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-140">In a scene with particularly bright lighting, print a code that is black on a gray background.</span></span> <span data-ttu-id="b0cc7-141">Dans une scène de faible luminosité, le noir sur blanc fonctionne.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-141">Under a low-light scene, black on white works.</span></span> <span data-ttu-id="b0cc7-142">De même, si le fond du code est particulièrement sombre, essayez un code noir en gris si votre taux de détection est faible.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-142">Likewise, if the backdrop to the code is particularly dark, try a black on gray code if your detection rate is low.</span></span> <span data-ttu-id="b0cc7-143">Dans le cas contraire, si le fond est plus clair, un code normal devrait fonctionner correctement.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-143">Otherwise, if the backdrop is lighter, a regular code should work fine.</span></span>

## <a name="qrtracking-api"></a><span data-ttu-id="b0cc7-144">API QRTracking</span><span class="sxs-lookup"><span data-stu-id="b0cc7-144">QRTracking API</span></span>

<span data-ttu-id="b0cc7-145">Le plug-in QRTracking expose les API pour le suivi du code QR.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-145">The QRTracking plugin exposes the APIs for QR code tracking.</span></span> <span data-ttu-id="b0cc7-146">Pour utiliser le plug-in, vous devrez utiliser les types suivants de l’espace de noms *QRCodesTrackerPlugin* .</span><span class="sxs-lookup"><span data-stu-id="b0cc7-146">To use the plugin, you will need to use the following types from the *QRCodesTrackerPlugin* namespace.</span></span>

```cs
 // QRTracker plugin namespace
 namespace QRCodesTrackerPlugin
 {
    // Encapsulates information about a labeled QR code element.
    public class QRCode
    {        
        // Unique id that identifies this QR code for this session.
        public Guid Id { get; private set; }
           
        // Version of this QR code.
        public Int32 Version { get; private set; }
        
        // PhysicalSizeMeters of this QR code.
        public float PhysicalSizeMeters { get; private set; }
        
        // QR code Data.
        public string Code { get; private set; }
        
        // QR code DataStream this is the error corrected data stream
        public Byte[] CodeStream { get; private set; }
        
        // QR code last detected QPC ticks.
        public Int64 LastDetectedQPCTicks { get; private set; }
    };
    
    // The type of a QR Code added event.
    public class QRCodeAddedEventArgs
    {   
        // Gets the QR Code that was added
        public QRCode Code { get; private set; }
    };
    
    // The type of a QR Code removed event.
    public class QRCodeRemovedEventArgs
    {
        // Gets the QR Code that was removed.
        public QRCode Code { get; private set; }
    };
    
    // The type of a QR Code updated event.
    public class QRCodeUpdatedEventArgs
    {
        // Gets the QR Code that was updated.
        public QRCode Code { get; private set; }
    };
    
    // A callback for handling the QR Code added event.
    public delegate void QRCodeAddedHandler(QRCodeAddedEventArgs args);
    
    // A callback for handling the QR Code removed event.
    public delegate void QRCodeRemovedHandler(QRCodeRemovedEventArgs args);
    
    // A callback for handling the QR Code updated event.
    public delegate void QRCodeUpdatedHandler(QRCodeUpdatedEventArgs args);
    
    // Enumerates the possible results of a start of QRTracker.
    public enum QRTrackerStartResult
    {
        // The start has succeeded.
        Success = 0,
        
        //  The currently no device is connected.
        DeviceNotConnected = 1,
        
        // The QRTracking Feature is not supported by the current HMD driver
        // systems
        FeatureNotSupported = 2,
        
        // The access is denide. Administrator needs to enable QR tracker feature.
        AccessDenied = 3,
    };
    
    // QRTracker
    public class QRTracker
    {
        // Constructs a new QRTracker.
        public QRTracker(){}
        
        // Gets the QRTracker.
        public static QRTracker Get()
        {
            return new QRTracker();
        }
        
        // Start the QRTracker. Returns QRTrackerStartResult.
        public QRTrackerStartResult Start()
        {
            throw new NotImplementedException();
        }
        
        // Stops tracking QR codes.
        public void Stop() {}

        // Not Implemented
        Windows.Foundation.Collections.IVector<QRCode> GetList() { throw new NotImplementedException(); }
        
        // Event representing the addition of a QR Code.
        public event QRCodeAddedHandler Added = delegate { };
        
        // Event representing the removal of a QR Code.
        public event QRCodeRemovedHandler Removed = delegate { };
        
        // Event representing the update of a QR Code.
        public event QRCodeUpdatedHandler Updated = delegate { };
    };
}
```

## <a name="implementing-qr-code-tracking-in-unity"></a><span data-ttu-id="b0cc7-147">Implémentation du suivi du code QR dans Unity</span><span class="sxs-lookup"><span data-stu-id="b0cc7-147">Implementing QR code tracking in Unity</span></span>

### <a name="sample-unity-scenes-in-mrtk-mixed-reality-toolkit"></a><span data-ttu-id="b0cc7-148">Exemples de scènes Unity dans MRTK (kit de préversion de réalité mixte)</span><span class="sxs-lookup"><span data-stu-id="b0cc7-148">Sample Unity scenes in MRTK (Mixed Reality Toolkit)</span></span>

<span data-ttu-id="b0cc7-149">Vous trouverez un exemple d’utilisation de l’API de suivi QR dans le [site github](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker)de la réalité mixte Toolkit.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-149">You can find an example for how to use the QR Tracking API in the Mixed Reality Toolkit [GitHub site](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker).</span></span>

<span data-ttu-id="b0cc7-150">MRTK a implémenté les scripts nécessaires pour simpilify l’utilisation du suivi QR.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-150">MRTK has implemented the needed scripts to simpilify the QR tracking usage.</span></span> <span data-ttu-id="b0cc7-151">Toutes les ressources nécessaires au développement d’applications de suivi QR se trouvent dans le dossier «QRTracker».</span><span class="sxs-lookup"><span data-stu-id="b0cc7-151">All necessary assets to develop QR tracking apps are in the "QRTracker" folder.</span></span> <span data-ttu-id="b0cc7-152">Il y a deux scènes: la première est un exemple pour afficher simplement les détails des codes QR tels qu’ils sont détectés, et le second montre comment utiliser le système de coordonnées attaché au code QR pour afficher des hologrammes.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-152">There are two scenes: the first is a sample to simply show details of the QR codes as they are detected, and the second demonstrates how to use the coordinate system attached to the QR code to display holograms.</span></span>
<span data-ttu-id="b0cc7-153">Un Prefab «QRScanner» a ajouté tous les scripts nécessaires pour utiliser QRCodes.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-153">There is a prefab "QRScanner" which added all the necessary scripts to the scenes to use QRCodes.</span></span> <span data-ttu-id="b0cc7-154">Le script QRCodeManager est une classe singleton qui implémente l’API QRCode.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-154">The script QRCodeManager is a singleton class that implements the QRCode API.</span></span> <span data-ttu-id="b0cc7-155">Cela doit être ajouté à votre scène.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-155">This needs to be added to your scene.</span></span> <span data-ttu-id="b0cc7-156">Le script «AttachToQRCode» est utilisé pour attacher des hologrammes aux systèmes de coordonnées du code QR, ce script peut être ajouté à l’un de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-156">The script "AttachToQRCode" is used to attach holograms to the QR Code coordinate systems, this script can be added to any of your holograms.</span></span> <span data-ttu-id="b0cc7-157">Le «SpatialGraphCoordinateSystem» montre comment utiliser le système de coordonnées QRCode.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-157">The "SpatialGraphCoordinateSystem" shows how to use the QRCode coordinate system.</span></span> <span data-ttu-id="b0cc7-158">Ces scripts peuvent être utilisés tels quels dans le cadre de votre projet, ou vous pouvez écrire vos propres scripts directement à l’aide du plug-in, comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-158">These scripts can be used as-is in your project scenes or you can write your own directly using the plugin as described above.</span></span>

### <a name="implementing-qr-code-tracking-in-unity-without-mrtk"></a><span data-ttu-id="b0cc7-159">Implémentation du suivi du code QR dans Unity sans MRTK</span><span class="sxs-lookup"><span data-stu-id="b0cc7-159">Implementing QR code tracking in Unity without MRTK</span></span>

<span data-ttu-id="b0cc7-160">Vous pouvez également utiliser l’API de suivi QR dans Unity sans dépendre de MRTK.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-160">You can also use the QR Tracking API in Unity without taking a dependency on MRTK.</span></span> <span data-ttu-id="b0cc7-161">Pour pouvoir utiliser l’API, vous devez préparer votre projet avec l’instruction suivante:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-161">In order to use the API, you will need to prepare your project with the following instruction:</span></span>

1. <span data-ttu-id="b0cc7-162">Créez un nouveau dossier dans le dossier composants de votre projet Unity avec le nom: «Plug-ins».</span><span class="sxs-lookup"><span data-stu-id="b0cc7-162">Create a new folder in the assets folder of your unity project with the name: "Plugins".</span></span>
2. <span data-ttu-id="b0cc7-163">Copiez tous les fichiers requis à partir de [ce dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) dans le dossier «Plug-ins» local que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-163">Copy all the required files from [this folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) into the local "Plugins" folder you just created.</span></span>
3. <span data-ttu-id="b0cc7-164">Vous pouvez utiliser les scripts de suivi QR dans le [dossier MRTK scripts](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) ou écrire le vôtre.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-164">You can use the QR tracking scripts in the [MRTK scripts folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) or write your own.</span></span>
<span data-ttu-id="b0cc7-165">Remarque : Ces plug-ins sont uniquement pour les builds [Windows 10 octobre 2018 Update (également appelées RS5)](release-notes-october-2018.md) .</span><span class="sxs-lookup"><span data-stu-id="b0cc7-165">Note: These plugins are only for [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md) builds.</span></span> <span data-ttu-id="b0cc7-166">Les plug-ins seront mis à jour avec la prochaine version de Windows.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-166">The plugins will be updated with the next windows release.</span></span> <span data-ttu-id="b0cc7-167">Les plug-ins actuels étaient expérimentaux et ne fonctionneront pas pour les versions ultérieures de Windows.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-167">The current plugins were experimental and will not work for future version of the windows.</span></span> <span data-ttu-id="b0cc7-168">De nouveaux plug-ins seront publiés et pourront être utilisés à partir de la prochaine version de Windows. ils ne seront pas pris en charge de façon descendante et ne fonctionneront pas avec RS5).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-168">New plugins will be published which can be used from next windows release and they will not be backwards compatable and will not work with RS5).</span></span>

## <a name="implementing-qr-code-tracking-in-directx"></a><span data-ttu-id="b0cc7-169">Implémentation du suivi du code QR dans DirectX</span><span class="sxs-lookup"><span data-stu-id="b0cc7-169">Implementing QR code tracking in DirectX</span></span>

<span data-ttu-id="b0cc7-170">Pour utiliser QRTrackingPlugin dans Visual Studio, vous devez ajouter la référence du QRTrackingPlugin au. winmd.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-170">To use the QRTrackingPlugin in Visual Studio, you will need to add reference of the QRTrackingPlugin to the .winmd.</span></span> <span data-ttu-id="b0cc7-171">Vous trouverez ici les [fichiers requis pour les plateformes prises en charge](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).</span><span class="sxs-lookup"><span data-stu-id="b0cc7-171">You can find the [required files for supported platforms here](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).</span></span>

```cpp
// MyClass.h
public ref class MyClass
{
    private:
      QRCodesTrackerPlugin::QRTracker^ m_qrtracker;
      // Handlers
      void OnAddedQRCode(QRCodesTrackerPlugin::QRCodeAddedEventArgs ^args);
      void OnUpdatedQRCode(QRCodesTrackerPlugin::QRCodeUpdatedEventArgs ^args);
      void OnRemovedQRCode(QRCodesTrackerPlugin::QRCodeRemovedEventArgs ^args);
    ..
};
```

```cpp
// MyClass.cpp
MyClass::MyClass()
{
    // Create the tracker and register the callbacks
    m_qrtracker = ref new QRCodesTrackerPlugin::QRTracker();
    m_qrtracker->Added += ref new QRCodesTrackerPlugin::QRCodeAddedHandler(this, &OnAddedQRCode);
    m_qrtracker->Updated += ref new QRCodesTrackerPlugin::QRCodeUpdatedHandler(this, &OnUpdatedQRCode);
    m_qrtracker->Removed += ref new QRCodesTrackerPlugin::QRCodeRemovedHandler(this, &QOnRemovedQRCode);

    // Start the tracker
    if (m_qrtracker->Start() != QRCodesTrackerPlugin::QRTrackerStartResult::Success)
    {
      // Handle the failure
      // It can fail for multiple reasons and can be handled properly 
    }
}

void MyClass::OnAddedQRCode(QRCodesTrackerPlugin::QRCodeAddedEventArgs ^args)
{
    // use args->Code add to own list  
}

void MyClass::OnUpdatedQRCode(QRCodesTrackerPlugin::QRCodeUpdatedEventArgs ^args)
{
    // use args->Code update the existing one with the new one in own list 
}

void MyClass::OnRemovedQRCode(QRCodesTrackerPlugin::QRCodeRemovedEventArgs ^args)
{
    // use args->Code remove from own list.
}
```

## <a name="getting-a-coordinate-system"></a><span data-ttu-id="b0cc7-172">Obtention d’un système de coordonnées</span><span class="sxs-lookup"><span data-stu-id="b0cc7-172">Getting a coordinate system</span></span>

<span data-ttu-id="b0cc7-173">Nous définissons un système de coordonnées de droite aligné avec le code QR dans l’angle supérieur gauche du carré de détection rapide dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-173">We define a right-hand coordinate system aligned with the QR code at the top left corner of the fast detection square in the top left.</span></span> <span data-ttu-id="b0cc7-174">Le système de coordonnées est illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-174">The coordinate system is shown below.</span></span> <span data-ttu-id="b0cc7-175">L’axe Z pointe sur le papier (non affiché), mais dans Unity, l’axe z est en dehors du papier et droitier.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-175">The Z-axis is pointing into the paper (not shown), but in Unity the z-axis is out of the paper and left-handed.</span></span>

<span data-ttu-id="b0cc7-176">Un SpatialCoordinateSystem est défini et aligné comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-176">A SpatialCoordinateSystem is defined that is aligned as shown.</span></span> <span data-ttu-id="b0cc7-177">Ce système de coordonnées peut être obtenu à partir de la plateforme à l’aide de l’API *Windows::P erception:: spatial::P Review:: SpatialGraphInteropPreview:: CreateCoordinateSystemForNode*.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-177">This coordinate system can be obtained from the platform using the API *Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode*.</span></span>

![Système de coordonnées du code QR](images/Qr-coordinatesystem.png) 

<span data-ttu-id="b0cc7-179">À partir de l’objet de code QRCode ^, le code suivant montre comment créer un rectangle et le placer dans le système de coordonnées QR:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-179">From QRCode^ Code object, the following code shows how to create a rectangle and put it in QR coordinate system:</span></span>

```cpp
// Creates a 2D rectangle in the x-y plane, with the specified properties.
std::vector<float3> SpatialStageManager::CreateRectangle(float width, float height)
{
    std::vector<float3> vertices(4);

    vertices[0] = { 0,  0, 0 };
    vertices[1] = { width,  0, 0 };
    vertices[2] = { width,  height, 0 };
    vertices[3] = { 0,  height, 0 };

    return vertices;
}
```

<span data-ttu-id="b0cc7-180">Vous pouvez utiliser la taille physique pour créer le rectangle QR:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-180">You can use the physical size to create the QR rectangle:</span></span>

```cpp
std::vector<float3> qrVertices = CreateRectangle(Code->PhysicalSizeMeters, Code->PhysicalSizeMeters); 
```

<span data-ttu-id="b0cc7-181">Le système de coordonnées peut être utilisé pour dessiner le code QR ou pour attacher des hologrammes à l’emplacement:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-181">The coordinate system can be used to draw the QR code or attach holograms to the location:</span></span>

```cpp
Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem = Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(Code->Id);
```

<span data-ttu-id="b0cc7-182">De même, votre *QRCodesTrackerPlugin:: QRCodeAddedHandler* peut se présenter comme suit:</span><span class="sxs-lookup"><span data-stu-id="b0cc7-182">Altogether, your *QRCodesTrackerPlugin::QRCodeAddedHandler* may look something like this:</span></span>

```cpp
void MyClass::OnAddedQRCode(QRCodesTrackerPlugin::QRCodeAddedEventArgs ^args)
{
    std::vector<float3> qrVertices = CreateRectangle(args->Code->PhysicalSizeMeters, args->Code->PhysicalSizeMeters);
    std::vector<unsigned short> qrCodeIndices = TriangulatePoints(qrVertices);
    XMFLOAT3 qrAreaColor = XMFLOAT3(DirectX::Colors::Aqua);

    Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem =  Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(args->Code->Id);
    std::shared_ptr<SceneObject> m_qrShape =
        std::make_shared<SceneObject>(
            m_deviceResources,
            reinterpret_cast<std::vector<XMFLOAT3>&>(qrVertices),
            qrCodeIndices,
            qrAreaColor,
            qrCoordinateSystem);

    m_sceneController->AddSceneObject(m_qrShape);
}
```

## <a name="troubleshooting-and-faq"></a><span data-ttu-id="b0cc7-183">Dépannage et FAQ</span><span class="sxs-lookup"><span data-stu-id="b0cc7-183">Troubleshooting and FAQ</span></span>

<span data-ttu-id="b0cc7-184">**Résolution des problèmes généraux**</span><span class="sxs-lookup"><span data-stu-id="b0cc7-184">**General troubleshooting**</span></span>

* <span data-ttu-id="b0cc7-185">Votre ordinateur exécute-t-il la mise à jour 2018 d’octobre de Windows 10?</span><span class="sxs-lookup"><span data-stu-id="b0cc7-185">Is your PC running the Windows 10 October 2018 Update?</span></span>
* <span data-ttu-id="b0cc7-186">Avez-vous défini la clé de Registre?</span><span class="sxs-lookup"><span data-stu-id="b0cc7-186">Have you set the reg key?</span></span> <span data-ttu-id="b0cc7-187">Redémarrage de l’appareil par la suite?</span><span class="sxs-lookup"><span data-stu-id="b0cc7-187">Restarted the device afterwards?</span></span>
* <span data-ttu-id="b0cc7-188">La version du code QR est-elle une version prise en charge?</span><span class="sxs-lookup"><span data-stu-id="b0cc7-188">Is the QR code version a supported version?</span></span> <span data-ttu-id="b0cc7-189">L’API actuelle prend en charge jusqu’à QR code version 20.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-189">Current API supports up to QR Code Version 20.</span></span> <span data-ttu-id="b0cc7-190">Nous vous recommandons d’utiliser la version 5 pour une utilisation générale.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-190">We recommend using version 5 for general usage.</span></span> 
* <span data-ttu-id="b0cc7-191">Êtes-vous suffisamment près du code QR?</span><span class="sxs-lookup"><span data-stu-id="b0cc7-191">Are you close enough to the QR code?</span></span> <span data-ttu-id="b0cc7-192">Plus la caméra est proche du code QR, plus la version de code QR que l’API peut prendre en charge est élevée.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-192">The closer the camera is to the QR code, the higher the QR code version the API can support.</span></span>  

<span data-ttu-id="b0cc7-193">**Comment puis-je fermer le code QR pour le détecter?**</span><span class="sxs-lookup"><span data-stu-id="b0cc7-193">**How close do I need to be to the QR code to detect it?**</span></span>

<span data-ttu-id="b0cc7-194">Cela dépend de la taille du code QR et de la version qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-194">This will depend on the size of the QR code, and also what version it is.</span></span> <span data-ttu-id="b0cc7-195">Pour un code QR de version 1 variant de 5 cm vers le côté de 25 cm, la distance de détection minimale est comprise entre 0,15 mètres et 0,5 mètres.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-195">For a version 1 QR code varying from 5 cm sides to 25 cm sides, the minimum detection distance ranges from 0.15 meters to 0.5 meters.</span></span> <span data-ttu-id="b0cc7-196">Les plus éloignées d’entre elles peuvent être détectées d’environ 0,3 mètres pour les plus petites cibles de code QR à 1,4 mètres pour la plus grande.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-196">The farthest away these can be detected from goes from about 0.3 meters for the smaller QR code targets to 1.4 meters for the bigger.</span></span> <span data-ttu-id="b0cc7-197">Pour les codes QR de plus grande taille, vous pouvez estimer; la distance de détection pour la taille augmente de façon linéaire.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-197">For QR codes bigger than that, you can estimate; the detection distance for size increases linearly.</span></span> <span data-ttu-id="b0cc7-198">Notre dispositif de suivi ne fonctionne pas avec les codes QR avec des bords inférieurs à 5 cm.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-198">Our tracker does not work with QR codes with sides smaller than 5 cm.</span></span>

<span data-ttu-id="b0cc7-199">**Les codes QR avec les logos fonctionnent-ils?**</span><span class="sxs-lookup"><span data-stu-id="b0cc7-199">**Do QR codes with logos work?**</span></span>

<span data-ttu-id="b0cc7-200">Les codes QR avec des logos n’ont pas été testés et ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-200">QR codes with logos have not been tested and are currently unsupported.</span></span>

<span data-ttu-id="b0cc7-201">**Comment faire effacer les codes QR de mon application afin qu’ils ne soient pas conservés?**</span><span class="sxs-lookup"><span data-stu-id="b0cc7-201">**How do I clear QR codes from my app so they don't persist?**</span></span>

* <span data-ttu-id="b0cc7-202">Les codes QR sont conservés uniquement dans la session de démarrage.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-202">QR codes are only persisted in the boot session.</span></span> <span data-ttu-id="b0cc7-203">Une fois que vous avez redémarré (ou redémarré le pilote), ceux-ci sont supprimés et détectés en tant que nouveaux objets la prochaine fois.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-203">Once you reboot (or restart the driver), they will be gone and detected as new objects next time.</span></span>
* <span data-ttu-id="b0cc7-204">L’historique du code QR est enregistré au niveau du système dans la session du pilote, mais vous pouvez configurer votre application pour qu’elle ignore les codes QR antérieurs à un horodateur spécifique si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-204">QR code history is saved at the system level in the driver session, but you can configure your app to ignore QR codes older than a specific timestamp if you want.</span></span> <span data-ttu-id="b0cc7-205">Actuellement, l’API prend en charge l’effacement de l’historique du code QR, car plusieurs applications peuvent être intéressées par les données.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-205">Currently the API does support clearing QR code history, as multiple apps might be interested in the data.</span></span>

<span data-ttu-id="b0cc7-206">**Les plug-ins pour RS5 et les versions ultérieures ne sont pas compatibles** La version RS5 du plug-in fonctionne uniquement pour RS5 et ne fonctionnera pas pour les futures versions.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-206">**The plugins for RS5 and future versions are not compatable** RS5 version of the plugin only works for RS5 and will not work for future versions.</span></span> <span data-ttu-id="b0cc7-207">Le plug-in expermental sera remplacé par le plug-in réel et devrait être celui que nous pouvons utiliser dans les futures versions de Windows.</span><span class="sxs-lookup"><span data-stu-id="b0cc7-207">The expermental plugin will be replaced with the real plugin and should be the one that we can use in future versions of the windows.</span></span>
