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
# <a name="qr-code-tracking"></a>Suivi du code QR

Le suivi du code QR est implémenté dans le pilote Windows Mixed Reality pour les casques immersif (VR). En activant le dispositif de suivi du code QR dans le pilote du casque, le casque balaie les codes QR et ils sont signalés aux applications intéressées. Cette fonctionnalité est disponible uniquement à partir de la [mise à jour 2018 de Windows 10 octobre (également appelée RS5)](release-notes-october-2018.md).

>[!NOTE]
>Les extraits de code de cet article illustrent actuellement l' C++utilisation de/CX plutôt que de C++/WinRT conforme C + +17, comme utilisé dans le [ C++ modèle de projet holographique](creating-a-holographic-directx-project.md).  Les concepts sont équivalents pour C++un projet/WinRT, bien que vous deviez traduire le code.

## <a name="device-support"></a>Prise en charge des appareils

<table>
    <colgroup>
    <col width="33%" />
    <col width="33%" />
    <col width="33%" />
    </colgroup>
    <tr>
        <td><strong>Fonctionnalité</strong></td>
        <td><a href="hololens-hardware-details.md"><strong>HoloLens</strong></a></td>
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques immersifs</strong></a></td>
    </tr>
     <tr>
        <td>Suivi du code QR</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="enabling-and-disabling-qr-code-tracking-for-your-headset"></a>Activation et désactivation du suivi du code QR pour votre casque
Remarque : Cette section est uniquement valide pour la [mise à jour 2018 de Windows 10 octobre (également appelée RS5)](release-notes-october-2018.md). À partir de 19h1 builds, vous n’aurez pas à le faire.
Que vous développiez une application de réalité mixte qui tire parti du suivi du code QR ou que vous soyez un client de l’une de ces applications, vous devez activer manuellement le suivi du code QR dans le pilote de votre casque.

Pour activer le **suivi du code QR** pour votre casque immersif:

1. Fermez l’application portail de réalité mixte sur votre PC.
2. Débranchez le casque de votre PC.
3. Exécutez le script suivant dans l’invite de commandes:<br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 1 /F`
4. Reconnectez votre casque à votre PC.

Pour désactiver le **suivi du code QR** pour votre casque immersif (VR):

1. Fermez l’application portail de réalité mixte sur votre PC.
2. Débranchez le casque de votre PC.
3. Exécutez le script suivant dans l’invite de commandes:<br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 0 /F`
4. Reconnectez votre casque à votre PC. Cela rendra les codes QR détectés «non localisables».

## <a name="printing-codes"></a>Codes d’impression

Tout d’abord, la [spécification des codes QR](https://www.qrcode.com/en/howto/code.html) indique «la zone de symboles de code QR nécessite une marge ou une «zone calme» autour de celle-ci pour être utilisée. La marge est une zone claire autour d’un symbole où rien n’est imprimé. Le code QR requiert une marge étendue à quatre modules sur tous les côtés d’un symbole.» Cela doit avoir une largeur, de chaque côté, de quatre fois la taille d’un module, un carré noir unique dans le code. La page spec contient des conseils sur la façon d’imprimer des codes QR et de déterminer la zone requise pour créer un code QR de taille spécifique.

Actuellement, la qualité de la détection du code QR est susceptible de varier l’éclairage et le fond. Pour combattre cela, Notez votre éclairage et imprimez le code approprié. Dans une scène avec un éclairage particulièrement clair, imprimez un code noir sur un arrière-plan gris. Dans une scène de faible luminosité, le noir sur blanc fonctionne. De même, si le fond du code est particulièrement sombre, essayez un code noir en gris si votre taux de détection est faible. Dans le cas contraire, si le fond est plus clair, un code normal devrait fonctionner correctement.

## <a name="qrtracking-api"></a>API QRTracking

Le plug-in QRTracking expose les API pour le suivi du code QR. Pour utiliser le plug-in, vous devrez utiliser les types suivants de l’espace de noms *QRCodesTrackerPlugin* .

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

## <a name="implementing-qr-code-tracking-in-unity"></a>Implémentation du suivi du code QR dans Unity

### <a name="sample-unity-scenes-in-mrtk-mixed-reality-toolkit"></a>Exemples de scènes Unity dans MRTK (kit de préversion de réalité mixte)

Vous trouverez un exemple d’utilisation de l’API de suivi QR dans le [site github](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker)de la réalité mixte Toolkit.

MRTK a implémenté les scripts nécessaires pour simpilify l’utilisation du suivi QR. Toutes les ressources nécessaires au développement d’applications de suivi QR se trouvent dans le dossier «QRTracker». Il y a deux scènes: la première est un exemple pour afficher simplement les détails des codes QR tels qu’ils sont détectés, et le second montre comment utiliser le système de coordonnées attaché au code QR pour afficher des hologrammes.
Un Prefab «QRScanner» a ajouté tous les scripts nécessaires pour utiliser QRCodes. Le script QRCodeManager est une classe singleton qui implémente l’API QRCode. Cela doit être ajouté à votre scène. Le script «AttachToQRCode» est utilisé pour attacher des hologrammes aux systèmes de coordonnées du code QR, ce script peut être ajouté à l’un de vos hologrammes. Le «SpatialGraphCoordinateSystem» montre comment utiliser le système de coordonnées QRCode. Ces scripts peuvent être utilisés tels quels dans le cadre de votre projet, ou vous pouvez écrire vos propres scripts directement à l’aide du plug-in, comme décrit ci-dessus.

### <a name="implementing-qr-code-tracking-in-unity-without-mrtk"></a>Implémentation du suivi du code QR dans Unity sans MRTK

Vous pouvez également utiliser l’API de suivi QR dans Unity sans dépendre de MRTK. Pour pouvoir utiliser l’API, vous devez préparer votre projet avec l’instruction suivante:

1. Créez un nouveau dossier dans le dossier composants de votre projet Unity avec le nom: «Plug-ins».
2. Copiez tous les fichiers requis à partir de [ce dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) dans le dossier «Plug-ins» local que vous venez de créer.
3. Vous pouvez utiliser les scripts de suivi QR dans le [dossier MRTK scripts](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) ou écrire le vôtre.
Remarque : Ces plug-ins sont uniquement pour les builds [Windows 10 octobre 2018 Update (également appelées RS5)](release-notes-october-2018.md) . Les plug-ins seront mis à jour avec la prochaine version de Windows. Les plug-ins actuels étaient expérimentaux et ne fonctionneront pas pour les versions ultérieures de Windows. De nouveaux plug-ins seront publiés et pourront être utilisés à partir de la prochaine version de Windows. ils ne seront pas pris en charge de façon descendante et ne fonctionneront pas avec RS5).

## <a name="implementing-qr-code-tracking-in-directx"></a>Implémentation du suivi du code QR dans DirectX

Pour utiliser QRTrackingPlugin dans Visual Studio, vous devez ajouter la référence du QRTrackingPlugin au. winmd. Vous trouverez ici les [fichiers requis pour les plateformes prises en charge](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).

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

## <a name="getting-a-coordinate-system"></a>Obtention d’un système de coordonnées

Nous définissons un système de coordonnées de droite aligné avec le code QR dans l’angle supérieur gauche du carré de détection rapide dans le coin supérieur gauche. Le système de coordonnées est illustré ci-dessous. L’axe Z pointe sur le papier (non affiché), mais dans Unity, l’axe z est en dehors du papier et droitier.

Un SpatialCoordinateSystem est défini et aligné comme indiqué. Ce système de coordonnées peut être obtenu à partir de la plateforme à l’aide de l’API *Windows::P erception:: spatial::P Review:: SpatialGraphInteropPreview:: CreateCoordinateSystemForNode*.

![Système de coordonnées du code QR](images/Qr-coordinatesystem.png) 

À partir de l’objet de code QRCode ^, le code suivant montre comment créer un rectangle et le placer dans le système de coordonnées QR:

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

Vous pouvez utiliser la taille physique pour créer le rectangle QR:

```cpp
std::vector<float3> qrVertices = CreateRectangle(Code->PhysicalSizeMeters, Code->PhysicalSizeMeters); 
```

Le système de coordonnées peut être utilisé pour dessiner le code QR ou pour attacher des hologrammes à l’emplacement:

```cpp
Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem = Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(Code->Id);
```

De même, votre *QRCodesTrackerPlugin:: QRCodeAddedHandler* peut se présenter comme suit:

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

## <a name="troubleshooting-and-faq"></a>Dépannage et FAQ

**Résolution des problèmes généraux**

* Votre ordinateur exécute-t-il la mise à jour 2018 d’octobre de Windows 10?
* Avez-vous défini la clé de Registre? Redémarrage de l’appareil par la suite?
* La version du code QR est-elle une version prise en charge? L’API actuelle prend en charge jusqu’à QR code version 20. Nous vous recommandons d’utiliser la version 5 pour une utilisation générale. 
* Êtes-vous suffisamment près du code QR? Plus la caméra est proche du code QR, plus la version de code QR que l’API peut prendre en charge est élevée.  

**Comment puis-je fermer le code QR pour le détecter?**

Cela dépend de la taille du code QR et de la version qu’il contient. Pour un code QR de version 1 variant de 5 cm vers le côté de 25 cm, la distance de détection minimale est comprise entre 0,15 mètres et 0,5 mètres. Les plus éloignées d’entre elles peuvent être détectées d’environ 0,3 mètres pour les plus petites cibles de code QR à 1,4 mètres pour la plus grande. Pour les codes QR de plus grande taille, vous pouvez estimer; la distance de détection pour la taille augmente de façon linéaire. Notre dispositif de suivi ne fonctionne pas avec les codes QR avec des bords inférieurs à 5 cm.

**Les codes QR avec les logos fonctionnent-ils?**

Les codes QR avec des logos n’ont pas été testés et ne sont actuellement pas pris en charge.

**Comment faire effacer les codes QR de mon application afin qu’ils ne soient pas conservés?**

* Les codes QR sont conservés uniquement dans la session de démarrage. Une fois que vous avez redémarré (ou redémarré le pilote), ceux-ci sont supprimés et détectés en tant que nouveaux objets la prochaine fois.
* L’historique du code QR est enregistré au niveau du système dans la session du pilote, mais vous pouvez configurer votre application pour qu’elle ignore les codes QR antérieurs à un horodateur spécifique si vous le souhaitez. Actuellement, l’API prend en charge l’effacement de l’historique du code QR, car plusieurs applications peuvent être intéressées par les données.

**Les plug-ins pour RS5 et les versions ultérieures ne sont pas compatibles** La version RS5 du plug-in fonctionne uniquement pour RS5 et ne fonctionnera pas pour les futures versions. Le plug-in expermental sera remplacé par le plug-in réel et devrait être celui que nous pouvons utiliser dans les futures versions de Windows.
