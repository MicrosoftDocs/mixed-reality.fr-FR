---
title: Code QR de suivi
description: Apprenez à activer sur le code QR de suivi pour votre casque (VR) immersive de réalité mixte Windows et implémenter la fonctionnalité dans vos applications de réalité virtuelle.
author: yoyozilla
ms.author: yoyoz
ms.date: 11/06/2018
ms.topic: article
keywords: VR, lbe, divertissement de basées sur l’emplacement, vr arcade, code qr d’arcade immersive, qr,
ms.openlocfilehash: b0f4480496c15f811979f76143acbd456d89e249
ms.sourcegitcommit: f7fc9afdf4632dd9e59bd5493e974e4fec412fc4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/13/2019
ms.locfileid: "59597132"
---
# <a name="qr-code-tracking"></a><span data-ttu-id="36843-104">Code QR de suivi</span><span class="sxs-lookup"><span data-stu-id="36843-104">QR code tracking</span></span>

<span data-ttu-id="36843-105">Code QR de suivi est implémenté dans le pilote Windows Mixed Reality pour des casques IMMERSIFS (VR).</span><span class="sxs-lookup"><span data-stu-id="36843-105">QR code tracking is implemented in the Windows Mixed Reality driver for immersive (VR) headsets.</span></span> <span data-ttu-id="36843-106">En activant le dispositif de suivi du code QR dans le pilote casque, le casque recherche les codes QR et elles sont signalées pour les applications concernées.</span><span class="sxs-lookup"><span data-stu-id="36843-106">By enabling the QR code tracker in the headset driver, the headset scans for QR codes and they are reported to interested apps.</span></span> <span data-ttu-id="36843-107">Cette fonctionnalité est uniquement disponible à partir de la [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md).</span><span class="sxs-lookup"><span data-stu-id="36843-107">This feature is only available as of the [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md).</span></span>

>[!NOTE]
><span data-ttu-id="36843-108">Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).</span><span class="sxs-lookup"><span data-stu-id="36843-108">The code snippets in this article currently demonstrate use of C++/CX rather than C++17-compliant C++/WinRT as used in the [C++ holographic project template](creating-a-holographic-directx-project.md).</span></span>  <span data-ttu-id="36843-109">Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.</span><span class="sxs-lookup"><span data-stu-id="36843-109">The concepts are equivalent for a C++/WinRT project, though you will need to translate the code.</span></span>

## <a name="device-support"></a><span data-ttu-id="36843-110">Prise en charge des appareils</span><span class="sxs-lookup"><span data-stu-id="36843-110">Device support</span></span>

<table>
<tr>
<th><span data-ttu-id="36843-111">Fonctionnalité</span><span class="sxs-lookup"><span data-stu-id="36843-111">Feature</span></span></th><th style="width:150px"> <span data-ttu-id="36843-112"><a href="hololens-hardware-details.md">HoloLens</a></span><span class="sxs-lookup"><span data-stu-id="36843-112"><a href="hololens-hardware-details.md">HoloLens</a></span></span></th><th style="width:150px"> <span data-ttu-id="36843-113"><a href="immersive-headset-hardware-details.md">Casques IMMERSIFS</a></span><span class="sxs-lookup"><span data-stu-id="36843-113"><a href="immersive-headset-hardware-details.md">Immersive headsets</a></span></span></th>
</tr><tr>
<td> <span data-ttu-id="36843-114">Code QR de suivi</span><span class="sxs-lookup"><span data-stu-id="36843-114">QR code tracking</span></span></td><td style="text-align: center;"></td><td style="text-align: center;"><span data-ttu-id="36843-115">✔️</span><span class="sxs-lookup"><span data-stu-id="36843-115">✔️</span></span></td>
</tr>
</table>

## <a name="enabling-and-disabling-qr-code-tracking-for-your-headset"></a><span data-ttu-id="36843-116">Activation et désactivation de QR code suivi pour votre casque</span><span class="sxs-lookup"><span data-stu-id="36843-116">Enabling and disabling QR code tracking for your headset</span></span>
<span data-ttu-id="36843-117">Remarque: Cette section est uniquement valide pour [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md).</span><span class="sxs-lookup"><span data-stu-id="36843-117">Note: This section is only valid for [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md).</span></span> <span data-ttu-id="36843-118">À partir de builds de 19h 1 et versions ultérieures vous ne devrez pas cela.</span><span class="sxs-lookup"><span data-stu-id="36843-118">From 19h1 builds onwards you will not have to do this.</span></span>
<span data-ttu-id="36843-119">Si vous développez une application de réalité mixte qui reposera sur code QR de suivi, ou si vous êtes un client d’un de ces applications, vous devez activer manuellement le code QR dans le pilote de votre casque de suivi.</span><span class="sxs-lookup"><span data-stu-id="36843-119">Whether you're developing a mixed reality app that will leverage QR code tracking, or you're a customer of one of these apps, you'll need to manually turn on QR code tracking in your headset's driver.</span></span>

<span data-ttu-id="36843-120">De **allumez le code QR suivi** pour votre immersive casque (VR) :</span><span class="sxs-lookup"><span data-stu-id="36843-120">In order to **turn on QR code tracking** for your immersive (VR) headset:</span></span>

1. <span data-ttu-id="36843-121">Fermez l’application de portail de réalité mixte sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-121">Close the Mixed Reality Portal app on your PC.</span></span>
2. <span data-ttu-id="36843-122">Débranchez le casque à partir de votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-122">Unplug the headset from your PC.</span></span>
3. <span data-ttu-id="36843-123">Dans l’invite de commandes, exécutez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="36843-123">Run the following script in the Command Prompt:</span></span><br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 1 /F`
4. <span data-ttu-id="36843-124">Se reconnecter votre casque à votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-124">Reconnect your headset to your PC.</span></span>

<span data-ttu-id="36843-125">Dans l’ordre aux **désactiver le code QR de suivi** pour votre immersive casque (VR) :</span><span class="sxs-lookup"><span data-stu-id="36843-125">In order to **turn off QR code tracking** for your immersive (VR) headset:</span></span>

1. <span data-ttu-id="36843-126">Fermez l’application de portail de réalité mixte sur votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-126">Close the Mixed Reality Portal app on your PC.</span></span>
2. <span data-ttu-id="36843-127">Débranchez le casque à partir de votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-127">Unplug the headset from your PC.</span></span>
3. <span data-ttu-id="36843-128">Dans l’invite de commandes, exécutez le script suivant :</span><span class="sxs-lookup"><span data-stu-id="36843-128">Run the following script in the Command Prompt:</span></span><br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 0 /F`
4. <span data-ttu-id="36843-129">Se reconnecter votre casque à votre PC.</span><span class="sxs-lookup"><span data-stu-id="36843-129">Reconnect your headset to your PC.</span></span> <span data-ttu-id="36843-130">Cela rendra les codes QR détectés « non localisables. »</span><span class="sxs-lookup"><span data-stu-id="36843-130">This will make any discovered QR codes "non-locatable."</span></span>

## <a name="printing-codes"></a><span data-ttu-id="36843-131">Codes de l’impression</span><span class="sxs-lookup"><span data-stu-id="36843-131">Printing codes</span></span>

<span data-ttu-id="36843-132">D’abord, le [spec pour les codes QR](https://www.qrcode.com/en/howto/code.html) indique que « la zone de symbole de Code QR nécessite une marge ou une « zone silencieux » autour de son utilisation.</span><span class="sxs-lookup"><span data-stu-id="36843-132">First and foremost, the [spec for QR codes](https://www.qrcode.com/en/howto/code.html) says "The QR Code symbol area requires a margin or "quiet zone" around it to be used.</span></span> <span data-ttu-id="36843-133">La marge est une effacer la zone autour d’un symbole où rien n’est imprimé.</span><span class="sxs-lookup"><span data-stu-id="36843-133">The margin is a clear area around a symbol where nothing is printed.</span></span> <span data-ttu-id="36843-134">Code QR nécessite une large marge de module de quatre à tous les côtés d’un symbole ».</span><span class="sxs-lookup"><span data-stu-id="36843-134">QR Code requires a four-module wide margin at all sides of a symbol."</span></span> <span data-ttu-id="36843-135">Cette opération doit avoir une largeur, sur chaque côté, de quatre fois la taille d’un module - un carré noir unique dans le code.</span><span class="sxs-lookup"><span data-stu-id="36843-135">This needs to have a width, on every side, of four times the size of a module - a single black square in the code.</span></span> <span data-ttu-id="36843-136">La page spec contient des conseils sur la façon d’imprimer des codes QR et de déterminer la zone requise pour effectuer une certain taille QR code.</span><span class="sxs-lookup"><span data-stu-id="36843-136">The spec page contains advice on how to print QR codes and figure out the area required to make a certain sized QR code.</span></span>

<span data-ttu-id="36843-137">Actuellement qualité de détection du code QR est vulnérable aux variables d’éclairage et filigrane.</span><span class="sxs-lookup"><span data-stu-id="36843-137">Currently QR code detection quality is susceptible to varying illumination and backdrop.</span></span> <span data-ttu-id="36843-138">Pour remédier à ce problème, notez votre d’éclairage et imprimer le code approprié.</span><span class="sxs-lookup"><span data-stu-id="36843-138">To combat this, note your illumination and print the appropriate code.</span></span> <span data-ttu-id="36843-139">Dans une scène avec particulièrement luminosité, imprimez un code qui est noir sur un fond gris.</span><span class="sxs-lookup"><span data-stu-id="36843-139">In a scene with particularly bright lighting, print a code that is black on a gray background.</span></span> <span data-ttu-id="36843-140">Sous une scène faible luminosité, noire sur blanc fonctionne.</span><span class="sxs-lookup"><span data-stu-id="36843-140">Under a low-light scene, black on white works.</span></span> <span data-ttu-id="36843-141">De même, si la toile de fond pour le code est particulièrement sombre, essayez un noir sur code grise si votre taux de détection est faible.</span><span class="sxs-lookup"><span data-stu-id="36843-141">Likewise, if the backdrop to the code is particularly dark, try a black on gray code if your detection rate is low.</span></span> <span data-ttu-id="36843-142">Sinon, si la toile de fond est plus clair, un code régulière devrait fonctionner sans problème.</span><span class="sxs-lookup"><span data-stu-id="36843-142">Otherwise, if the backdrop is lighter, a regular code should work fine.</span></span>

## <a name="qrtracking-api"></a><span data-ttu-id="36843-143">QRTracking API</span><span class="sxs-lookup"><span data-stu-id="36843-143">QRTracking API</span></span>

<span data-ttu-id="36843-144">Le plug-in QRTracking expose les API pour le code QR de suivi.</span><span class="sxs-lookup"><span data-stu-id="36843-144">The QRTracking plugin exposes the APIs for QR code tracking.</span></span> <span data-ttu-id="36843-145">Pour utiliser le plug-in, vous devez utiliser les types suivants à partir de la *QRCodesTrackerPlugin* espace de noms.</span><span class="sxs-lookup"><span data-stu-id="36843-145">To use the plugin, you will need to use the following types from the *QRCodesTrackerPlugin* namespace.</span></span>

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

## <a name="implementing-qr-code-tracking-in-unity"></a><span data-ttu-id="36843-146">Implémentation de code QR suivi des modifications dans Unity</span><span class="sxs-lookup"><span data-stu-id="36843-146">Implementing QR code tracking in Unity</span></span>

### <a name="sample-unity-scenes-in-mrtk-mixed-reality-toolkit"></a><span data-ttu-id="36843-147">Exemples de séquences de Unity dans MRTK (Toolkit de réalité mixte)</span><span class="sxs-lookup"><span data-stu-id="36843-147">Sample Unity scenes in MRTK (Mixed Reality Toolkit)</span></span>

<span data-ttu-id="36843-148">Vous trouverez un exemple pour savoir comment utiliser l’API de suivi QR dans le Toolkit de réalité mixte [site GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker).</span><span class="sxs-lookup"><span data-stu-id="36843-148">You can find an example for how to use the QR Tracking API in the Mixed Reality Toolkit [GitHub site](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker).</span></span>

<span data-ttu-id="36843-149">MRTK a implémenté les scripts nécessaires pour simpilify le suivi de l’utilisation de QR.</span><span class="sxs-lookup"><span data-stu-id="36843-149">MRTK has implemented the needed scripts to simpilify the QR tracking usage.</span></span> <span data-ttu-id="36843-150">Toutes les ressources nécessaires pour développer QR suivi des applications sont dans le dossier « QRTracker ».</span><span class="sxs-lookup"><span data-stu-id="36843-150">All necessary assets to develop QR tracking apps are in the "QRTracker" folder.</span></span> <span data-ttu-id="36843-151">Il existe deux scènes : le premier est un exemple pour illustrer simplement les détails des codes QR comme ils sont détectés, et le second montre comment utiliser le système de coordonnées associé au code QR pour afficher les hologrammes.</span><span class="sxs-lookup"><span data-stu-id="36843-151">There are two scenes: the first is a sample to simply show details of the QR codes as they are detected, and the second demonstrates how to use the coordinate system attached to the QR code to display holograms.</span></span>
<span data-ttu-id="36843-152">Il existe un QRScanner « prefab » qui ajouté tous les scrips nécessaires à l’arrière-plan à utiliser QRCodes.</span><span class="sxs-lookup"><span data-stu-id="36843-152">There is a prefab "QRScanner" which added all the necessary scrips to the scenes to use QRCodes.</span></span> <span data-ttu-id="36843-153">Le script QRCodeManager est une classe singileton qui implémente l’API QRCode vous pouvez l’ajouter à la scène de vous.</span><span class="sxs-lookup"><span data-stu-id="36843-153">The script QRCodeManager is a singileton class that implements the QRCode API you can add it to you scene.</span></span> <span data-ttu-id="36843-154">Les scripts « AttachToQRCode » est utilisé pour joindre hologrammes aux systèmes coodridnate Code QR, ce script peut être ajouté à un de vos hologrammes.</span><span class="sxs-lookup"><span data-stu-id="36843-154">The scripts "AttachToQRCode" is used to attach holograms to the QR Code coodridnate systems, this script can be added to any of your holograms.</span></span> <span data-ttu-id="36843-155">Le « SpatialGraphCoordinateSystem » montre comment utiliser le système de coordonnées QRCode.</span><span class="sxs-lookup"><span data-stu-id="36843-155">The "SpatialGraphCoordinateSystem" shows how to use the QRCode coordinate system.</span></span> <span data-ttu-id="36843-156">Ces scripts peuvent être utilisés en l’état dans les scènes de votre projet ou vous pouvez écrire votre propre directement en utilisant le plug-in comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="36843-156">These scripts can be used as is in your project scenes or you can write your own directly using the plugin as described above.</span></span>

### <a name="implementing-qr-code-tracking-in-unity-without-mrtk"></a><span data-ttu-id="36843-157">Implémentation de code QR dans Unity sans MRTK de suivi</span><span class="sxs-lookup"><span data-stu-id="36843-157">Implementing QR code tracking in Unity without MRTK</span></span>

<span data-ttu-id="36843-158">Vous pouvez également utiliser l’API de suivi QR dans Unity sans dépendance envers MRTK.</span><span class="sxs-lookup"><span data-stu-id="36843-158">You can also use the QR Tracking API in Unity without taking a dependency on MRTK.</span></span> <span data-ttu-id="36843-159">Pour pouvoir utiliser l’API, vous devez préparer votre projet avec l’instruction suivante :</span><span class="sxs-lookup"><span data-stu-id="36843-159">In order to use the API, you will need to prepare your project with the following instruction:</span></span>

1. <span data-ttu-id="36843-160">Créer un nouveau dossier dans le dossier de ressources de votre projet unity avec le nom : « Plug-ins ».</span><span class="sxs-lookup"><span data-stu-id="36843-160">Create a new folder in the assets folder of your unity project with the name: "Plugins".</span></span>
2. <span data-ttu-id="36843-161">Copie tous les fichiers requis à partir de [ce dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) dans le dossier « Plug-ins » local que vous venez de créer.</span><span class="sxs-lookup"><span data-stu-id="36843-161">Copy all the required files from [this folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) into the local "Plugins" folder you just created.</span></span>
3. <span data-ttu-id="36843-162">Vous pouvez utiliser le QR suivi des scripts dans le [dossier de scripts MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) ou écrivez votre propre.</span><span class="sxs-lookup"><span data-stu-id="36843-162">You can use the QR tracking scripts in the [MRTK scripts folder](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) or write your own.</span></span>
<span data-ttu-id="36843-163">Remarque: Ces plug-ins sont uniquement pour [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md) génère.</span><span class="sxs-lookup"><span data-stu-id="36843-163">Note: These plugins are only for [Windows 10 October 2018 Update (also known as RS5)](release-notes-october-2018.md) builds.</span></span> <span data-ttu-id="36843-164">Les plug-ins mettra à jour avec la prochaine version de windows.</span><span class="sxs-lookup"><span data-stu-id="36843-164">The plugins will be updated with the next windows release.</span></span> <span data-ttu-id="36843-165">Les plug-ins actuels ont été expérimentales et ne fonctionnent pas pour une future version de windows.</span><span class="sxs-lookup"><span data-stu-id="36843-165">The current plugins were experimental and will not work for future version of the windows.</span></span> <span data-ttu-id="36843-166">Nouveaux plug-ins paraîtra qui peut être utilisé à partir de la prochaine version de windows et ils ne seront pas descendante compatible et ne fonctionneront pas avec RS5).</span><span class="sxs-lookup"><span data-stu-id="36843-166">New plugins will be published which can be used from next windows release and they will not be backwards compatable and will not work with RS5).</span></span>

## <a name="implementing-qr-code-tracking-in-directx"></a><span data-ttu-id="36843-167">Implémentation de code QR suivi des modifications dans DirectX</span><span class="sxs-lookup"><span data-stu-id="36843-167">Implementing QR code tracking in DirectX</span></span>

<span data-ttu-id="36843-168">Pour utiliser le QRTrackingPlugin dans Visual Studio, vous devrez ajouter la référence de la QRTrackingPlugin à la .winmd.</span><span class="sxs-lookup"><span data-stu-id="36843-168">To use the QRTrackingPlugin in Visual Studio, you will need to add reference of the QRTrackingPlugin to the .winmd.</span></span> <span data-ttu-id="36843-169">Vous pouvez trouver la [les fichiers requis pour les plateformes prises en charge ici](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).</span><span class="sxs-lookup"><span data-stu-id="36843-169">You can find the [required files for supported platforms here](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).</span></span>

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

## <a name="getting-a-coordinate-system"></a><span data-ttu-id="36843-170">Obtention d’un système de coordonnées</span><span class="sxs-lookup"><span data-stu-id="36843-170">Getting a coordinate system</span></span>

<span data-ttu-id="36843-171">Nous définissons un système de coordonnées droite aligné avec le code QR dans le coin supérieur gauche du carré de détection rapide dans le coin supérieur gauche.</span><span class="sxs-lookup"><span data-stu-id="36843-171">We define a right-hand coordinate system aligned with the QR code at the top left corner of the fast detection square in the top left.</span></span> <span data-ttu-id="36843-172">Le système de coordonnées est présenté ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="36843-172">The coordinate system is shown below.</span></span> <span data-ttu-id="36843-173">L’axe z pointe dans le document (non illustré), mais dans Unity, l’axe des z est en dehors de papier et gaucher.</span><span class="sxs-lookup"><span data-stu-id="36843-173">The Z-axis is pointing into the paper (not shown), but in Unity the z-axis is out of the paper and left-handed.</span></span>

<span data-ttu-id="36843-174">Un SpatialCoordinateSystem est définie qui est aligné comme indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="36843-174">A SpatialCoordinateSystem is defined that is aligned as shown.</span></span> <span data-ttu-id="36843-175">Ce système de coordonnées peut être obtenu à partir de la plateforme à l’aide de l’API *Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode*.</span><span class="sxs-lookup"><span data-stu-id="36843-175">This coordinate system can be obtained from the platform using the API *Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode*.</span></span>

![Système de coordonnées de code QR](images/Qr-coordinatesystem.png) 

<span data-ttu-id="36843-177">À partir de QRCode ^ Code objet, le code suivant montre comment créer un rectangle et placez-le dans le système de coordonnées QR :</span><span class="sxs-lookup"><span data-stu-id="36843-177">From QRCode^ Code object, the following code shows how to create a rectangle and put it in QR coordinate system:</span></span>

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

<span data-ttu-id="36843-178">Vous pouvez utiliser la taille physique pour créer le rectangle QR :</span><span class="sxs-lookup"><span data-stu-id="36843-178">You can use the physical size to create the QR rectangle:</span></span>

```cpp
std::vector<float3> qrVertices = CreateRectangle(Code->PhysicalSizeMeters, Code->PhysicalSizeMeters); 
```

<span data-ttu-id="36843-179">Le système de coordonnées peut être utilisé pour dessiner le code QR ou attacher hologrammes à l’emplacement :</span><span class="sxs-lookup"><span data-stu-id="36843-179">The coordinate system can be used to draw the QR code or attach holograms to the location:</span></span>

```cpp
Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem = Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(Code->Id);
```

<span data-ttu-id="36843-180">Purement et simplement votre *QRCodesTrackerPlugin::QRCodeAddedHandler* peut ressembler à ceci :</span><span class="sxs-lookup"><span data-stu-id="36843-180">Altogether, your *QRCodesTrackerPlugin::QRCodeAddedHandler* may look something like this:</span></span>

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

## <a name="troubleshooting-and-faq"></a><span data-ttu-id="36843-181">Résolution des problèmes et Forum aux questions</span><span class="sxs-lookup"><span data-stu-id="36843-181">Troubleshooting and FAQ</span></span>

<span data-ttu-id="36843-182">**Résolution des problèmes généraux**</span><span class="sxs-lookup"><span data-stu-id="36843-182">**General troubleshooting**</span></span>

* <span data-ttu-id="36843-183">Est votre PC exécutant Windows 10 octobre 2018 mettre à jour ?</span><span class="sxs-lookup"><span data-stu-id="36843-183">Is your PC running the Windows 10 October 2018 Update?</span></span>
* <span data-ttu-id="36843-184">Vous avez défini la clé de Registre ?</span><span class="sxs-lookup"><span data-stu-id="36843-184">Have you set the reg key?</span></span> <span data-ttu-id="36843-185">Redémarrage de l’appareil par la suite ?</span><span class="sxs-lookup"><span data-stu-id="36843-185">Restarted the device afterwards?</span></span>
* <span data-ttu-id="36843-186">Est la version du code QR à une version prise en charge ?</span><span class="sxs-lookup"><span data-stu-id="36843-186">Is the QR code version a supported version?</span></span> <span data-ttu-id="36843-187">Prend en charge l’API actuelle jusqu'à 20 de Version de Code QR.</span><span class="sxs-lookup"><span data-stu-id="36843-187">Current API supports up to QR Code Version 20.</span></span> <span data-ttu-id="36843-188">Nous vous recommandons d’utiliser la version 5 pour une utilisation générale.</span><span class="sxs-lookup"><span data-stu-id="36843-188">We recommend using version 5 for general usage.</span></span> 
* <span data-ttu-id="36843-189">Sont suffisamment pour le code QR ?</span><span class="sxs-lookup"><span data-stu-id="36843-189">Are you close enough to the QR code?</span></span> <span data-ttu-id="36843-190">L’appareil photo est proche du code QR, plus la QR code version l’API peut prendre en charge.</span><span class="sxs-lookup"><span data-stu-id="36843-190">The closer the camera is to the QR code, the higher the QR code version the API can support.</span></span>  

<span data-ttu-id="36843-191">**Comment fermer doivent-ils être pour le code QR détecte ?**</span><span class="sxs-lookup"><span data-stu-id="36843-191">**How close do I need to be to the QR code to detect it?**</span></span>

<span data-ttu-id="36843-192">Cela dépend de la taille du code QR et également quelle version se.</span><span class="sxs-lookup"><span data-stu-id="36843-192">This will depend on the size of the QR code, and also what version it is.</span></span> <span data-ttu-id="36843-193">Pour un code QR de version 1 comprise entre les côtés 5 cm aux côtés de 25 cm, la distance minimale détection allant de 0,15 mètres à 0,5 mètres.</span><span class="sxs-lookup"><span data-stu-id="36843-193">For a version 1 QR code varying from 5 cm sides to 25 cm sides, the minimum detection distance ranges from 0.15 meters to 0.5 meters.</span></span> <span data-ttu-id="36843-194">Le plus éloigné disparaître ces peuvent être détectés à partir de va environ 0,3 mètres pour les cibles de code QR plus petits à 1,4 mètres pour le plus grand.</span><span class="sxs-lookup"><span data-stu-id="36843-194">The farthest away these can be detected from goes from about 0.3 meters for the smaller QR code targets to 1.4 meters for the bigger.</span></span> <span data-ttu-id="36843-195">Pour les codes QR supérieures à celles, vous pouvez estimer ; la distance de détection pour la taille augmente de façon linéaire.</span><span class="sxs-lookup"><span data-stu-id="36843-195">For QR codes bigger than that, you can estimate; the detection distance for size increases linearly.</span></span> <span data-ttu-id="36843-196">Notre mise hors tension ne fonctionne pas avec les codes QR avec côtés inférieure à 5 cm.</span><span class="sxs-lookup"><span data-stu-id="36843-196">Our tracker does not work with QR codes with sides smaller than 5 cm.</span></span>

<span data-ttu-id="36843-197">**Faire des codes QR avec un travail de logos ?**</span><span class="sxs-lookup"><span data-stu-id="36843-197">**Do QR codes with logos work?**</span></span>

<span data-ttu-id="36843-198">Codes QR avec logos n’ont pas été testés et sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="36843-198">QR codes with logos have not been tested and are currently unsupported.</span></span>

<span data-ttu-id="36843-199">**Comment effacer les codes QR à partir de mon application afin qu’ils ne persistent pas ?**</span><span class="sxs-lookup"><span data-stu-id="36843-199">**How do I clear QR codes from my app so they don't persist?**</span></span>

* <span data-ttu-id="36843-200">Codes QR sont uniquement conservées dans la session de démarrage.</span><span class="sxs-lookup"><span data-stu-id="36843-200">QR codes are only persisted in the boot session.</span></span> <span data-ttu-id="36843-201">Une fois que vous redémarrez (ou le pilote), ils seront disparus et détectés en tant que la prochaine fois que de nouveaux objets.</span><span class="sxs-lookup"><span data-stu-id="36843-201">Once you reboot (or restart the driver), they will be gone and detected as new objects next time.</span></span>
* <span data-ttu-id="36843-202">Historique de code QR est enregistré au niveau du système dans la session de pilote, mais vous pouvez configurer votre application pour ignorer les codes QR antérieurs à un horodatage spécifique si vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="36843-202">QR code history is saved at the system level in the driver session, but you can configure your app to ignore QR codes older than a specific timestamp if you want.</span></span> <span data-ttu-id="36843-203">Actuellement l’API ne prend pas en charge l’historique de code QR d’effacement, comme plusieurs applications peuvent être intéressées par les données.</span><span class="sxs-lookup"><span data-stu-id="36843-203">Currently the API does support clearing QR code history, as multiple apps might be interested in the data.</span></span>

<span data-ttu-id="36843-204">**Les plug-ins pour RS5 et les versions ultérieures ne sont pas compatible** version RS5 du plug-in fonctionne uniquement pour les RS5 et ne fonctionnera pas pour les versions futures.</span><span class="sxs-lookup"><span data-stu-id="36843-204">**The plugins for RS5 and future versions are not compatable** RS5 version of the plugin only works for RS5 and will not work for future versions.</span></span> <span data-ttu-id="36843-205">Le plug-in expermental sera remplacé par le plug-in réels et doit être celui que nous pouvons utiliser dans les futures versions de windows.</span><span class="sxs-lookup"><span data-stu-id="36843-205">The expermental plugin will be replaced with the real plugin and should be the one that we can use in future versions of the windows.</span></span>
