---
title: Code QR de suivi
description: Apprenez à activer sur le code QR de suivi pour votre casque (VR) immersive de réalité mixte Windows et implémenter la fonctionnalité dans vos applications de réalité virtuelle.
author: yoyozilla
ms.author: yoyoz
ms.date: 11/06/2018
ms.topic: article
keywords: VR, lbe, divertissement de basées sur l’emplacement, vr arcade, code qr d’arcade immersive, qr,
ms.openlocfilehash: 465056cf645a8b9dc9e0e2d3f9dacf887df67c52
ms.sourcegitcommit: 17f86fed532d7a4e91bd95baca05930c4a5c68c5
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/11/2019
ms.locfileid: "66829981"
---
# <a name="qr-code-tracking"></a>Code QR de suivi

Code QR de suivi est implémenté dans le pilote Windows Mixed Reality pour des casques IMMERSIFS (VR). En activant le dispositif de suivi du code QR dans le pilote casque, le casque recherche les codes QR et elles sont signalées pour les applications concernées. Cette fonctionnalité est uniquement disponible à partir de la [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md).

>[!NOTE]
>Actuellement les extraits de code dans cet article illustrent l’utilisation de C++/CX plutôt que C ++ 17-conformes C++/WinRT tel qu’utilisé dans le [ C++ modèle de projet HOLOGRAPHIQUE](creating-a-holographic-directx-project.md).  Les concepts sont équivalentes pour un C++/WinRT de projet, même si vous devez traduire le code.

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
        <td><a href="immersive-headset-hardware-details.md"><strong>Casques IMMERSIFS</strong></a></td>
    </tr>
     <tr>
        <td>Code QR de suivi</td>
        <td>❌</td>
        <td>✔️</td>
    </tr>
</table>

## <a name="enabling-and-disabling-qr-code-tracking-for-your-headset"></a>Activation et désactivation de QR code suivi pour votre casque
Remarque: Cette section est uniquement valide pour [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md). À partir de builds de 19h 1 et versions ultérieures vous ne devrez pas cela.
Si vous développez une application de réalité mixte qui reposera sur code QR de suivi, ou si vous êtes un client d’un de ces applications, vous devez activer manuellement le code QR dans le pilote de votre casque de suivi.

De **allumez le code QR suivi** pour votre immersive casque (VR) :

1. Fermez l’application de portail de réalité mixte sur votre PC.
2. Débranchez le casque à partir de votre PC.
3. Dans l’invite de commandes, exécutez le script suivant :<br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 1 /F`
4. Se reconnecter votre casque à votre PC.

Dans l’ordre aux **désactiver le code QR de suivi** pour votre immersive casque (VR) :

1. Fermez l’application de portail de réalité mixte sur votre PC.
2. Débranchez le casque à partir de votre PC.
3. Dans l’invite de commandes, exécutez le script suivant :<br>
    `reg add "HKLM\SOFTWARE\Microsoft\HoloLensSensors" /v  EnableQRTrackerDefault /t REG_DWORD /d 0 /F`
4. Se reconnecter votre casque à votre PC. Cela rendra les codes QR détectés « non localisables. »

## <a name="printing-codes"></a>Codes de l’impression

D’abord, le [spec pour les codes QR](https://www.qrcode.com/en/howto/code.html) indique que « la zone de symbole de Code QR nécessite une marge ou une « zone silencieux » autour de son utilisation. La marge est une effacer la zone autour d’un symbole où rien n’est imprimé. Code QR nécessite une large marge de module de quatre à tous les côtés d’un symbole ». Cette opération doit avoir une largeur, sur chaque côté, de quatre fois la taille d’un module - un carré noir unique dans le code. La page spec contient des conseils sur la façon d’imprimer des codes QR et de déterminer la zone requise pour effectuer une certain taille QR code.

Actuellement qualité de détection du code QR est vulnérable aux variables d’éclairage et filigrane. Pour remédier à ce problème, notez votre d’éclairage et imprimer le code approprié. Dans une scène avec particulièrement luminosité, imprimez un code qui est noir sur un fond gris. Sous une scène faible luminosité, noire sur blanc fonctionne. De même, si la toile de fond pour le code est particulièrement sombre, essayez un noir sur code grise si votre taux de détection est faible. Sinon, si la toile de fond est plus clair, un code régulière devrait fonctionner sans problème.

## <a name="qrtracking-api"></a>QRTracking API

Le plug-in QRTracking expose les API pour le code QR de suivi. Pour utiliser le plug-in, vous devez utiliser les types suivants à partir de la *QRCodesTrackerPlugin* espace de noms.

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

## <a name="implementing-qr-code-tracking-in-unity"></a>Implémentation de code QR suivi des modifications dans Unity

### <a name="sample-unity-scenes-in-mrtk-mixed-reality-toolkit"></a>Exemples de séquences de Unity dans MRTK (Toolkit de réalité mixte)

Vous trouverez un exemple pour savoir comment utiliser l’API de suivi QR dans le Toolkit de réalité mixte [site GitHub](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker).

MRTK a implémenté les scripts nécessaires pour simpilify le suivi de l’utilisation de QR. Toutes les ressources nécessaires pour développer QR suivi des applications sont dans le dossier « QRTracker ». Il existe deux scènes : le premier est un exemple pour illustrer simplement les détails des codes QR comme ils sont détectés, et le second montre comment utiliser le système de coordonnées associé au code QR pour afficher les hologrammes.
Il existe un QRScanner « prefab » qui ajoute tous les scripts nécessaires à l’arrière-plan à utiliser QRCodes. Le script QRCodeManager est une classe singleton qui implémente l’API QRCode. Cette opération doit être ajouté à votre scène. Le script « AttachToQRCode » est utilisé pour attacher hologrammes pour les systèmes de coordonnées de Code QR, ce script peut être ajouté à un de vos hologrammes. Le « SpatialGraphCoordinateSystem » montre comment utiliser le système de coordonnées QRCode. Ces scripts peuvent être utilisés en tant que-est dans votre projet scènes ou vous pouvez écrire votre propre directement en utilisant le plug-in comme décrit ci-dessus.

### <a name="implementing-qr-code-tracking-in-unity-without-mrtk"></a>Implémentation de code QR dans Unity sans MRTK de suivi

Vous pouvez également utiliser l’API de suivi QR dans Unity sans dépendance envers MRTK. Pour pouvoir utiliser l’API, vous devez préparer votre projet avec l’instruction suivante :

1. Créer un nouveau dossier dans le dossier de ressources de votre projet unity avec le nom : « Plug-ins ».
2. Copie tous les fichiers requis à partir de [ce dossier](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins) dans le dossier « Plug-ins » local que vous venez de créer.
3. Vous pouvez utiliser le QR suivi des scripts dans le [dossier de scripts MRTK](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Scripts) ou écrivez votre propre.
Remarque: Ces plug-ins sont uniquement pour [mise à jour 10 octobre 2018 Windows (également appelé RS5)](release-notes-october-2018.md) génère. Les plug-ins mettra à jour avec la prochaine version de windows. Les plug-ins actuels ont été expérimentales et ne fonctionnent pas pour une future version de windows. Nouveaux plug-ins paraîtra qui peut être utilisé à partir de la prochaine version de windows et ils ne seront pas descendante compatible et ne fonctionneront pas avec RS5).

## <a name="implementing-qr-code-tracking-in-directx"></a>Implémentation de code QR suivi des modifications dans DirectX

Pour utiliser le QRTrackingPlugin dans Visual Studio, vous devrez ajouter la référence de la QRTrackingPlugin à la .winmd. Vous pouvez trouver la [les fichiers requis pour les plateformes prises en charge ici](https://github.com/Microsoft/MixedRealityToolkit-Unity/tree/htk_release/Assets/HoloToolkit-Preview/QRTracker/Plugins/WSA).

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

Nous définissons un système de coordonnées droite aligné avec le code QR dans le coin supérieur gauche du carré de détection rapide dans le coin supérieur gauche. Le système de coordonnées est présenté ci-dessous. L’axe z pointe dans le document (non illustré), mais dans Unity, l’axe des z est en dehors de papier et gaucher.

Un SpatialCoordinateSystem est définie qui est aligné comme indiqué ci-dessous. Ce système de coordonnées peut être obtenu à partir de la plateforme à l’aide de l’API *Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode*.

![Système de coordonnées de code QR](images/Qr-coordinatesystem.png) 

À partir de QRCode ^ Code objet, le code suivant montre comment créer un rectangle et placez-le dans le système de coordonnées QR :

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

Vous pouvez utiliser la taille physique pour créer le rectangle QR :

```cpp
std::vector<float3> qrVertices = CreateRectangle(Code->PhysicalSizeMeters, Code->PhysicalSizeMeters); 
```

Le système de coordonnées peut être utilisé pour dessiner le code QR ou attacher hologrammes à l’emplacement :

```cpp
Windows::Perception::Spatial::SpatialCoordinateSystem^ qrCoordinateSystem = Windows::Perception::Spatial::Preview::SpatialGraphInteropPreview::CreateCoordinateSystemForNode(Code->Id);
```

Purement et simplement votre *QRCodesTrackerPlugin::QRCodeAddedHandler* peut ressembler à ceci :

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

## <a name="troubleshooting-and-faq"></a>Résolution des problèmes et Forum aux questions

**Résolution des problèmes généraux**

* Est votre PC exécutant Windows 10 octobre 2018 mettre à jour ?
* Vous avez défini la clé de Registre ? Redémarrage de l’appareil par la suite ?
* Est la version du code QR à une version prise en charge ? Prend en charge l’API actuelle jusqu'à 20 de Version de Code QR. Nous vous recommandons d’utiliser la version 5 pour une utilisation générale. 
* Sont suffisamment pour le code QR ? L’appareil photo est proche du code QR, plus la QR code version l’API peut prendre en charge.  

**Comment fermer doivent-ils être pour le code QR détecte ?**

Cela dépend de la taille du code QR et également quelle version se. Pour un code QR de version 1 comprise entre les côtés 5 cm aux côtés de 25 cm, la distance minimale détection allant de 0,15 mètres à 0,5 mètres. Le plus éloigné disparaître ces peuvent être détectés à partir de va environ 0,3 mètres pour les cibles de code QR plus petits à 1,4 mètres pour le plus grand. Pour les codes QR supérieures à celles, vous pouvez estimer ; la distance de détection pour la taille augmente de façon linéaire. Notre mise hors tension ne fonctionne pas avec les codes QR avec côtés inférieure à 5 cm.

**Faire des codes QR avec un travail de logos ?**

Codes QR avec logos n’ont pas été testés et sont actuellement pas pris en charge.

**Comment effacer les codes QR à partir de mon application afin qu’ils ne persistent pas ?**

* Codes QR sont uniquement conservées dans la session de démarrage. Une fois que vous redémarrez (ou le pilote), ils seront disparus et détectés en tant que la prochaine fois que de nouveaux objets.
* Historique de code QR est enregistré au niveau du système dans la session de pilote, mais vous pouvez configurer votre application pour ignorer les codes QR antérieurs à un horodatage spécifique si vous le souhaitez. Actuellement l’API ne prend pas en charge l’historique de code QR d’effacement, comme plusieurs applications peuvent être intéressées par les données.

**Les plug-ins pour RS5 et les versions ultérieures ne sont pas compatible** version RS5 du plug-in fonctionne uniquement pour les RS5 et ne fonctionnera pas pour les versions futures. Le plug-in expermental sera remplacé par le plug-in réels et doit être celui que nous pouvons utiliser dans les futures versions de windows.
