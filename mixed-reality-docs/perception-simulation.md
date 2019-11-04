---
title: Simulation de perception
description: Guide d’utilisation de la bibliothèque de simulation de perception pour automatiser une entrée simulée pour des applications immersifs
author: pbarnettms
ms.author: pbarnett
ms.date: 04/26/2019
ms.topic: article
keywords: HoloLens, simulation, test
ms.openlocfilehash: 503533bc5a2e9307b7c5217632d42670285aac0a
ms.sourcegitcommit: 6bc6757b9b273a63f260f1716c944603dfa51151
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/01/2019
ms.locfileid: "73437546"
---
# <a name="perception-simulation"></a>Simulation de perception

Voulez-vous créer un test automatisé pour votre application ? Voulez-vous que vos tests vont au-delà des tests unitaires au niveau du composant et pour vraiment exercer votre application de bout en bout ? La simulation de perception correspond à ce que vous recherchez. La bibliothèque de simulation de perception envoie des données d’entrée humaines et mondiales à votre application afin que vous puissiez automatiser vos tests. Par exemple, vous pouvez simuler l’entrée d’un utilisateur cherchant à une position renouvelée et spécifique, puis d’effectuer un mouvement ou d’utiliser un contrôleur de mouvement.

La simulation de perception peut envoyer une entrée simulée comme celle-ci à un HoloLens physique, à l’émulateur HoloLens (1ère génération), à l’émulateur HoloLens 2 ou à un PC avec portail de réalité mixte installé. La simulation de perception contourne les capteurs actifs sur un appareil de réalité mixte et envoie une entrée simulée aux applications qui s’exécutent sur l’appareil. Les applications reçoivent ces événements d’entrée via les mêmes API qu’ils utilisent toujours et ne peuvent pas indiquer la différence entre l’exécution avec des capteurs réels et l’exécution avec la simulation de perception. La simulation de perception est la même technologie que celle utilisée par les émulateurs HoloLens pour envoyer une entrée simulée à la machine virtuelle HoloLens.

Pour commencer à utiliser la simulation dans votre code, commencez par créer un objet IPerceptionSimulationManager. À partir de cet objet, vous pouvez émettre des commandes pour contrôler les propriétés d’un « humain » simulé, y compris la position de la tête, la position de la main et les gestes, et vous pouvez activer et manipuler les contrôleurs de mouvement.

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a>Configuration d’un projet Visual Studio pour la simulation de perception
1. [Installez l’émulateur HoloLens](install-the-tools.md) sur votre PC de développement. L’émulateur comprend les bibliothèques que vous allez utiliser pour la simulation de perception.
2. Créez un projet de bureau C# Visual Studio (un projet de console fonctionne bien pour commencer).
3. Ajoutez les fichiers binaires suivants à votre projet en tant que références (Project-> Add-> Reference...). Vous pouvez les trouver dans% ProgramFiles (x86)% \ Microsoft XDE\\(version), par exemple **% ProgramFiles (x86)% \ Microsoft XDE\\10.0.18362.0** pour l’émulateur HoloLens 2.  (Remarque : bien que les fichiers binaires fassent partie de l’émulateur HoloLens 2, ils fonctionnent également pour Windows Mixed Reality sur le bureau.) un. PerceptionSimulationManager. Interop. dll-wrapper C# managé pour la simulation de perception.
    b. PerceptionSimulationRest. dll-Library pour la configuration d’un canal de communication de sockets Web vers le HoloLens ou l’émulateur.
    c. SimulationStream. Interop. dll : types partagés pour la simulation.
4. Ajoutez le fichier binaire d’implémentation PerceptionSimulationManager. dll à votre projet a. Tout d’abord, ajoutez-le en tant que fichier binaire au projet (Project-> Ajouter > élément existant...). Enregistrez-le en tant que lien afin qu’il ne soit pas copié dans le dossier source de votre projet. ![ajouter PerceptionSimulationManager. dll au projet sous la forme d’un lien](images/saveaslink.png) b. Ensuite, assurez-vous qu’il est copié dans votre dossier de sortie lors de la génération. Il s’agit de la feuille de propriétés pour le binaire. ![Marquez PerceptionSimulationManager. dll pour copier dans le répertoire de sortie](images/copyalways.png)
5. Définissez la plateforme de votre solution active sur x64.  (Utilisez la Configuration Manager pour créer une entrée de plateforme pour x64, si elle n’existe pas déjà.)

## <a name="creating-an-iperceptionsimulation-manager-object"></a>Création d’un objet IPerceptionSimulation Manager

Pour contrôler la simulation, vous allez émettre des mises à jour des objets récupérés à partir d’un objet IPerceptionSimulationManager. La première étape consiste à obtenir cet objet et à le connecter à votre appareil ou émulateur cible. Vous pouvez récupérer l’adresse IP de votre émulateur en cliquant sur le bouton du portail de l’appareil dans la [barre d’outils](using-the-hololens-emulator.md) .

![icône Ouvrir le portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail**de l’appareil : Ouvrez le portail de périphériques Windows pour le système d’exploitation HoloLens dans l’émulateur.  Pour Windows Mixed Reality, vous pouvez le récupérer dans l’application paramètres sous « mettre à jour & sécurité », puis « pour les développeurs » dans la section « se connecter à l’aide de » sous « activer le portail d’appareils ».  Veillez à noter l’adresse IP et le port.

Tout d’abord, vous devez appeler RestSimulationStreamSink. Create pour obtenir un objet RestSimulationStreamSink. Il s’agit de l’appareil ou de l’émulateur cible que vous allez contrôler sur une connexion http. Vos commandes sont transmises à et gérées par le [portail de périphériques Windows](using-the-windows-device-portal.md) exécuté sur l’appareil ou l’émulateur. Les quatre paramètres dont vous avez besoin pour créer un objet sont les suivants :
* URI Uri : adresse IP de l’appareil cible (par exemple, « https://123.123.123.123 » ou « https://123.123.123.123:50080 »)
* Informations d’identification System .net. NetworkCredential-nom d’utilisateur/mot de passe pour la connexion au [portail d’appareils Windows](using-the-windows-device-portal.md) sur l’appareil ou l’émulateur cible. Si vous vous connectez à l’émulateur via son adresse locale (par exemple,*168...* *) sur le même PC, toutes les informations d’identification seront acceptées.
* bool normal-true pour la priorité normale, false pour basse priorité. Vous souhaitez généralement définir cette propriété sur *true* pour les scénarios de test, ce qui permet à votre test de prendre le contrôle.  La simulation de l’émulateur et de la réalité mixte Windows utilise des connexions de faible priorité.  Si votre test utilise également une connexion de faible priorité, la connexion établie le plus récemment sera Control.
* Jeton-jeton System. Threading. CancellationToken pour annuler l’opération asynchrone.

Ensuite, vous allez créer le IPerceptionSimulationManager. Il s’agit de l’objet que vous utilisez pour contrôler la simulation. Notez que cela doit également être fait dans une méthode Async.

## <a name="control-the-simulated-human"></a>Contrôler l’homme simulé

Un IPerceptionSimulationManager a une propriété humaine qui retourne un objet ISimulatedHuman. Pour contrôler l’homme simulé, effectuez des opérations sur cet objet. Exemple :

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a>Exemple C# d’application console de base

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            Task.Run(async () =>
            {
                RestSimulationStreamSink sink = null;
                CancellationToken token = new System.Threading.CancellationToken();

                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }

                // Always close the sink to return control to the previous application.
                if (sink != null)
                {
                    await sink.Close(token);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();
        }
    }
}
```

## <a name="extended-sample-c-console-application"></a>Exemple C# d’application console étendue

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.PerceptionSimulation;

namespace ConsoleApplication1
{
    class Program
    {
        static void Main(string[] args)
        {
            RestSimulationStreamSink sink = null;
            CancellationToken token = new System.Threading.CancellationToken();

            Task.Run(async () =>
            {
                try
                {
                    sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("https://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        token);

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);

                    // Now, we'll simulate a sequence of actions.
                    // Sleeps in-between each action give time to the system
                    // to be able to properly react.
                    // This is just an example. A proper automated test should verify
                    // that the app has behaved correctly
                    // before proceeding to the next step, instead of using Sleeps.

                    // Activate the right hand
                    manager.Human.RightHand.Activated = true;

                    // Simulate Bloom gesture, which should cause Shell to disappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... this time, Shell should reappear
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);

                    // Simulate a Head rotation down around the X axis
                    // This should cause gaze to aim about the center of the screen
                    manager.Human.Head.Rotate(new Rotation3(0.04f, 0.0f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a finger press & release
                    // Should cause a tap on the center tile, thus launching it
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate a second finger press & release
                    // Should activate the app that was launched when the center tile was clicked
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(5000);

                    // Simulate a Head rotation towards the upper right corner
                    manager.Human.Head.Rotate(new Rotation3(-0.14f, 0.17f, 0.0f));
                    Thread.Sleep(300);

                    // Simulate a third finger press & release
                    // Should press the Remove button on the app
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerPressed);
                    Thread.Sleep(300);
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.FingerReleased);
                    Thread.Sleep(2000);

                    // Simulate Bloom gesture again... bringing the Shell back once more
                    manager.Human.RightHand.PerformGesture(SimulatedGesture.Home);
                    Thread.Sleep(2000);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
                }
            });

            // If main exits, the process exits.  
            Console.WriteLine("Press any key to exit...");
            Console.ReadLine();

            // Always close the sink to return control to the previous application.
            if (sink != null)
            {
                sink.Close(token);
            }
        }
    }
}
```

## <a name="note-on-6-dof-controllers"></a>Remarque sur les contrôleurs 6-DDL

Avant d’appeler des propriétés sur des méthodes sur un contrôleur 6-DDL simulé, vous devez activer le contrôleur.  Si ce n’est pas le cas, une exception est générée.  À compter de la mise à jour de Windows 10 2019 mai, les contrôleurs 6-DDL simulés peuvent être installés et activés en définissant la propriété Status sur l’objet ISimulatedSixDofController sur SimulatedSixDofControllerStatus. active.
Dans la mise à jour 2018 de Windows 10 octobre et les versions antérieures, vous devez d’abord installer séparément un contrôleur 6-DDL simulé en appelant l’outil PerceptionSimulationDevice situé dans le dossier \Windows\System32.  L’utilisation de cet outil est la suivante :


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

Par exemple,

```
    PerceptionSimulationDevice.exe i 6dof 1
```

Les actions prises en charge sont les suivantes :
* i = installation
* q = requête
* r = supprimer

Les instances prises en charge sont les suivantes :
* 1 = le contrôleur 6-DDL de gauche
* 2 = le contrôleur 6-DDL correct

Le code de sortie du processus indique la réussite (valeur de retour zéro) ou l’échec (valeur de retour différente de zéro).  Lorsque vous utilisez l’action q pour demander si un contrôleur est installé ou non, la valeur de retour est zéro (0) si le contrôleur n’est pas déjà installé ou un (1) si le contrôleur est installé.

Lorsque vous supprimez un contrôleur sur la mise à jour 2018 de Windows 10 octobre ou une version antérieure, définissez son état sur OFF via l’API en premier, puis appelez l’outil PerceptionSimulationDevice.

Notez que cet outil doit être exécuté en tant qu’administrateur.




## <a name="api-reference"></a>Référence de l’API

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a>Microsoft. PerceptionSimulation. SimulatedDeviceType

Décrit un type d’appareil simulé

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

**Microsoft. PerceptionSimulation. SimulatedDeviceType. Reference**

Un appareil de référence fictif, la valeur par défaut pour PerceptionSimulationManager

### <a name="microsoftperceptionsimulationheadtrackermode"></a>Microsoft. PerceptionSimulation. HeadTrackerMode

Décrit un mode de suivi d’en-tête

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

**Microsoft. PerceptionSimulation. HeadTrackerMode. default**

Suivi des en-têtes par défaut. Cela signifie que le système peut sélectionner le mode de suivi optimal en fonction des conditions d’exécution.

**Microsoft. PerceptionSimulation. HeadTrackerMode. orientation**

Suivi d’en-tête d’orientation uniquement. Cela signifie que la position suivie peut ne pas être fiable, et certaines fonctionnalités qui dépendent de la position de la tête peuvent ne pas être disponibles.

**Microsoft. PerceptionSimulation. HeadTrackerMode. position**

Suivi de l’en-tête positionnel. Cela signifie que la position et l’orientation de la tête de suivi sont fiables

### <a name="microsoftperceptionsimulationsimulatedgesture"></a>Microsoft. PerceptionSimulation. SimulatedGesture

Décrit un mouvement simulé

```
public enum SimulatedGesture
{
    None = 0,
    FingerPressed = 1,
    FingerReleased = 2,
    Home = 4,
    Max = Home
}
```

**Microsoft. PerceptionSimulation. SimulatedGesture. None**

Valeur de sentinelle utilisée pour indiquer l’absence de gestes.

**Microsoft. PerceptionSimulation. SimulatedGesture. FingerPressed**

Mouvement appuyé sur le doigt.

**Microsoft. PerceptionSimulation. SimulatedGesture. FingerReleased**

Mouvement de libération d’un doigt.

**Microsoft. PerceptionSimulation. SimulatedGesture. orig**

Mouvement de démarrage/système.

**Microsoft. PerceptionSimulation. SimulatedGesture. Max**

Mouvement maximal valide.

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a>Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus

États possibles d’un contrôleur 6-DDL simulé.

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. OFF**

Le contrôleur 6-DDL est désactivé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. active**

Le contrôleur 6-DDL est activé et suivi.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. TrackingLost**

Le contrôleur 6-DDL est activé, mais ne peut pas être suivi.

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a>Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton

Les boutons pris en charge sur un contrôleur 6-DDL simulé.

```
public enum SimulatedSixDofControllerButton
{
    None = 0,
    Home = 1,
    Menu = 2,
    Grip = 4,
    TouchpadPress = 8,
    Select = 16,
    TouchpadTouch = 32,
    Thumbstick = 64,
    Max = Thumbstick
}
```

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. None**

Valeur de sentinelle utilisée pour indiquer qu’aucun bouton n’est présent.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. orig**

Le bouton d’hébergement est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. menu**

Le bouton de menu est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. poignée**

Le bouton de la poignée est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadPress**

Le pavé tactile est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Select**

Le bouton Sélectionner est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadTouch**

Le pavé tactile est touché.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Stick**

Le stick analogique est enfoncé.

**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Max**

Le bouton nombre maximal valide.


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a>Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState

État d’étalonnage des yeux simulés

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. non disponible**

L’étalonnage des yeux n’est pas disponible.

**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Ready**

Les yeux ont été étalonnés.  Il s'agit de la valeur par défaut.

**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Configuration**

Les yeux sont calibrés.

**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. UserCalibrationNeeded**

Les yeux doivent être étalonnés.

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a>Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy

Précision de suivi d’une jointure de la main.

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. non disponible**

La jointure n’est pas suivie.

**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. approximatif**

La position conjointe est déduite.

**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. visible**

L’articulation est entièrement suivie.

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a>Microsoft. PerceptionSimulation. SimulatedHandPose

Précision de suivi d’une jointure de la main.

```
public enum SimulatedHandPose
{
    Closed = 0,
    Open = 1,
    Point = 2,
    Pinch = 3,
    Max = Pinch
}
```

**Microsoft. PerceptionSimulation. SimulatedHandPose. Closed**

Les jointures Finger de la main sont configurées pour refléter une pose fermée.

**Microsoft. PerceptionSimulation. SimulatedHandPose. Open**

Les jointures Finger de la main sont configurées pour refléter une pose ouverte.

**Microsoft. PerceptionSimulation. SimulatedHandPose. point**

Les jointures Finger de la main sont configurées pour refléter une pose de pointage.

**Microsoft. PerceptionSimulation. SimulatedHandPose. pincement**

Les jointures Finger de la main sont configurées pour refléter une pose de pincement.

**Microsoft. PerceptionSimulation. SimulatedHandPose. Max**

Valeur maximale valide pour SimulatedHandPose.


### <a name="microsoftperceptionsimulationplaybackstate"></a>Microsoft. PerceptionSimulation. PlaybackState

Décrit l’état d’une lecture.

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

**Microsoft. PerceptionSimulation. PlaybackState. Stopped**

L’enregistrement est actuellement arrêté et prêt pour la lecture.

**Microsoft. PerceptionSimulation. PlaybackState. Playing**

L’enregistrement est en cours de diffusion.

**Microsoft. PerceptionSimulation. PlaybackState. Paused**

L’enregistrement est actuellement suspendu.

**Microsoft. PerceptionSimulation. PlaybackState. end**

L’enregistrement a atteint la fin.

### <a name="microsoftperceptionsimulationvector3"></a>Microsoft. PerceptionSimulation. Vector3

Décrit un vecteur de 3 composants, qui peut décrire un point ou un vecteur dans l’espace 3D.

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

**Microsoft. PerceptionSimulation. Vector3. X**

Composant X du vecteur.

**Microsoft. PerceptionSimulation. Vector3. Y**

Composant Y du vecteur.

**Microsoft. PerceptionSimulation. Vector3. Z**

Composant Z du vecteur.

**Microsoft. PerceptionSimulation. Vector3. #ctor (System. Single, System. Single, System. Single)**

Construisez un nouveau Vector3.

Paramètres
* x-composant x du vecteur.
* y : composant y du vecteur.
* z-composant z du vecteur.

### <a name="microsoftperceptionsimulationrotation3"></a>Microsoft. PerceptionSimulation. Rotation3

Décrit une rotation de 3 composants.

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

**Microsoft. PerceptionSimulation. Rotation3. brai**

Composant de pas de la rotation, en hauteur autour de l’axe X.

**Microsoft. PerceptionSimulation. Rotation3. lacet**

Composant de lacet de la rotation, à droite autour de l’axe Y.

**Microsoft. PerceptionSimulation. Rotation3. Roll**

Composant de roulement de la rotation, à droite autour de l’axe Z.

**Microsoft. PerceptionSimulation. Rotation3. #ctor (System. Single, System. Single, System. Single)**

Construisez un nouveau Rotation3.

Paramètres
* tangage : composant de pas de la rotation.
* lacet : composant de lacet de la rotation.
* Roll-le composant Roll de la rotation.

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a>Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration

Décrit la configuration d’un joint sur une main simulée.

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. position**

Position de la jointure.

**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. rotation**

Rotation de la jointure.

**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. TrackingAccuracy**

Précision de suivi de la jointure.


### <a name="microsoftperceptionsimulationfrustum"></a>Microsoft. PerceptionSimulation. frustum

Décrit un frustum d’affichage, tel qu’il est généralement utilisé par un appareil photo.

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

**Microsoft. PerceptionSimulation. frustum. Near**

Distance minimale contenue dans le frustum.

**Microsoft. PerceptionSimulation. frustum. Far**

Distance maximale contenue dans le frustum.

**Microsoft. PerceptionSimulation. frustum. FieldOfView**

Champ horizontal de la vue de frustum, en radians (inférieur à PI).

**Microsoft. PerceptionSimulation. frustum. AspectRatio**

Rapport entre le champ horizontal de la vue et le champ vertical de l’affichage.

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a>Microsoft. PerceptionSimulation. IPerceptionSimulationManager

Racine pour la génération des paquets utilisés pour contrôler un appareil.

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Device**

Récupérez l’objet d’appareil simulé qui interprète l’homme simulé et le monde simulé.

**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Human**

Récupérez l’objet qui contrôle l’homme simulé.

**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Reset**

Rétablit l’État par défaut de la simulation.

### <a name="microsoftperceptionsimulationisimulateddevice"></a>Microsoft. PerceptionSimulation. ISimulatedDevice

Interface décrivant l’appareil qui interprète le monde simulé et l’homme simulé

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

**Microsoft. PerceptionSimulation. ISimulatedDevice. HeadTracker**

Récupérez le dispositif de suivi des têtes à partir de l’appareil simulé.

**Microsoft. PerceptionSimulation. ISimulatedDevice. HandTracker**

Récupérez le dispositif de suivi de main à partir de l’appareil simulé.

**Microsoft. PerceptionSimulation. ISimulatedDevice. SetSimulatedDeviceType (Microsoft. PerceptionSimulation. SimulatedDeviceType)**

Définissez les propriétés de l’appareil simulé pour qu’elles correspondent au type d’appareil fourni.

Paramètres
* type-le nouveau type d’appareil simulé

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a>Microsoft. PerceptionSimulation. ISimulatedHeadTracker

Interface décrivant la partie de l’appareil simulé qui effectue le suivi du chef de l’homme simulé.

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

**Microsoft. PerceptionSimulation. ISimulatedHeadTracker. HeadTrackerMode**

Récupère et définit le mode de suivi d’en-tête actuel.

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a>Microsoft. PerceptionSimulation. ISimulatedHandTracker

Interface décrivant la partie de l’appareil simulé qui effectue le suivi des mains de l’homme simulé

```
public interface ISimulatedHandTracker
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    float Pitch { get; set; }
    bool FrustumIgnored { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    Frustum Frustum { get; set; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedHandTracker. WorldPosition**

Récupérer la position du nœud par rapport au monde, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedHandTracker. position**

Récupère et définit la position du suivi de la main simulé, par rapport au centre de l’en-tête.

**Microsoft. PerceptionSimulation. ISimulatedHandTracker. brai**

Récupérer et définir le pas à pas bas du suivi simulé.

**Microsoft. PerceptionSimulation. ISimulatedHandTracker. FrustumIgnored**

Récupérez et définissez si le frustum du suivi de la main simulé est ignoré. Lorsqu’ils sont ignorés, les deux mains sont toujours visibles. Lorsqu’elles ne sont pas ignorées (par défaut), elles ne sont visibles que lorsqu’elles se trouvent dans le frustum du dispositif de suivi de la main.

**Microsoft. PerceptionSimulation. ISimulatedHandTracker. frustum**

Récupérez et définissez les propriétés frustum utilisées pour déterminer si les mains sont visibles pour le suivi de la main simulé.

### <a name="microsoftperceptionsimulationisimulatedhuman"></a>Microsoft. PerceptionSimulation. ISimulatedHuman

Interface de niveau supérieur pour le contrôle de l’homme simulé.

```
public interface ISimulatedHuman 
{
    Vector3 WorldPosition { get; set; }
    float Direction { get; set; }
    float Height { get; set; }
    ISimulatedHand LeftHand { get; }
    ISimulatedHand RightHand { get; }
    ISimulatedHead Head { get; }
    void Move(Vector3 translation);
    void Rotate(float radians);
}
```

**Microsoft. PerceptionSimulation. ISimulatedHuman. WorldPosition**

Récupérer et définir la position du nœud par rapport au monde, en mètres. La position correspond à un point au centre des pieds de l’homme.

**Microsoft. PerceptionSimulation. ISimulatedHuman. direction**

Récupérez et définissez le sens des visages humains simulés dans le monde. 0 radians est confronté à l’axe Z négatif. Les radians positifs pivotent dans le sens des aiguilles d’une montre autour de l’axe Y.

**Microsoft. PerceptionSimulation. ISimulatedHuman. Height**

Récupérez et définissez la hauteur de l’homme simulé, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedHuman. LeftHand**

Récupérez la main gauche de l’homme simulé.

**Microsoft. PerceptionSimulation. ISimulatedHuman. à droite**

Récupérez la main droite de l’homme simulé.

**Microsoft. PerceptionSimulation. ISimulatedHuman. Head**

Récupérez l’en-tête de l’homme simulé.

**Microsoft. PerceptionSimulation. ISimulatedHuman. Move (Microsoft. PerceptionSimulation. Vector3)**

Déplacer le humain simulé par rapport à sa position actuelle, en mètres.

Paramètres
* translation : translation à déplacer, par rapport à la position actuelle.

**Microsoft. PerceptionSimulation. ISimulatedHuman. Rotate (System. Single)**

Faire pivoter l’homme simulé par rapport à sa direction actuelle, dans le sens des aiguilles d’une montre autour de l’axe Y

Paramètres
* radians-la valeur de rotation autour de l’axe Y.

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a>Microsoft. PerceptionSimulation. ISimulatedHuman2

Des propriétés supplémentaires sont disponibles en convertissant le ISimulatedHuman en ISimulatedHuman2

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedHuman2. LeftController**

Récupérez le contrôleur 6-DDL de gauche.

**Microsoft. PerceptionSimulation. ISimulatedHuman2. RightController**

Récupérez le contrôleur 6-DDL approprié.


### <a name="microsoftperceptionsimulationisimulatedhand"></a>Microsoft. PerceptionSimulation. ISimulatedHand

Interface décrivant une main de l’homme simulé

```
public interface ISimulatedHand
{
    Vector3 WorldPosition { get; }
    Vector3 Position { get; set; }
    bool Activated { [return: MarshalAs(UnmanagedType.Bool)] get; [param: MarshalAs(UnmanagedType.Bool)] set; }
    bool Visible { [return: MarshalAs(UnmanagedType.Bool)] get; }
    void EnsureVisible();
    void Move(Vector3 translation);
    void PerformGesture(SimulatedGesture gesture);
}
```

**Microsoft. PerceptionSimulation. ISimulatedHand. WorldPosition**

Récupérer la position du nœud par rapport au monde, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedHand. position**

Récupérer et définir la position de la main simulée par rapport à l’homme, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedHand. Activated**

Récupère et définit si la main est actuellement activée.

**Microsoft. PerceptionSimulation. ISimulatedHand. visible**

Récupère si la main est actuellement visible pour le SimulatedDevice (IE, si elle se trouve dans une position à détecter par le HandTracker).

**Microsoft. PerceptionSimulation. ISimulatedHand. EnsureVisible**

Déplacez la main de manière à ce qu’elle soit visible par le SimulatedDevice.

**Microsoft. PerceptionSimulation. ISimulatedHand. Move (Microsoft. PerceptionSimulation. Vector3)**

Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.

Paramètres
* translation-le montant pour traduire la main simulée.

**Microsoft. PerceptionSimulation. ISimulatedHand. PerformGesture (Microsoft. PerceptionSimulation. SimulatedGesture)**

Effectuez un mouvement à l’aide de la main simulée.  Elle sera détectée uniquement par le système si la main est activée.

Paramètres
* geste : mouvement à effectuer.

### <a name="microsoftperceptionsimulationisimulatedhand2"></a>Microsoft. PerceptionSimulation. ISimulatedHand2

Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand2.
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedHand2. orientation**

Récupère ou définit la rotation de la main simulée.  Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.

### <a name="microsoftperceptionsimulationisimulatedhand3"></a>Microsoft. PerceptionSimulation. ISimulatedHand3

Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand3
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

**Microsoft. PerceptionSimulation. ISimulatedHand3. GetJointConfiguration**

Obtient la configuration conjointe pour l’articulation spécifiée.

**Microsoft. PerceptionSimulation. ISimulatedHand3. SetJointConfiguration**

Définit la configuration conjointe pour l’articulation spécifiée.

**Microsoft. PerceptionSimulation. ISimulatedHand3. SetHandPose**

Définissez la main sur une pose connue avec un indicateur facultatif à animer.  Remarque : l’animation ne permettra pas aux jointures de refléter immédiatement leurs configurations conjointes finales.


### <a name="microsoftperceptionsimulationisimulatedhead"></a>Microsoft. PerceptionSimulation. ISimulatedHead

Interface décrivant l’en-tête de l’homme simulé.

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

**Microsoft. PerceptionSimulation. ISimulatedHead. WorldPosition**

Récupérer la position du nœud par rapport au monde, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedHead. rotation**

Récupère la rotation de la tête simulée. Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.

**Microsoft. PerceptionSimulation. ISimulatedHead. diametre**

Récupérer le diamètre de la tête simulée. Cette valeur est utilisée pour déterminer le centre de l’en-tête (point de rotation).

**Microsoft. PerceptionSimulation. ISimulatedHead. Rotate (Microsoft. PerceptionSimulation. Rotation3)**

Faire pivoter la tête simulée par rapport à sa rotation actuelle. Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.

Paramètres
* rotation : quantité à faire pivoter.

### <a name="microsoftperceptionsimulationisimulatedhead2"></a>Microsoft. PerceptionSimulation. ISimulatedHead2

Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHead en ISimulatedHead2

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedHead2. Eyes**

Récupérez les yeux de l’homme simulé.

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a>Microsoft. PerceptionSimulation. ISimulatedSixDofController

Interface décrivant un contrôleur 6-DDL associé à l’homme simulé.

```
public interface ISimulatedSixDofController
{
    Vector3 WorldPosition { get; }
    SimulatedSixDofControllerStatus Status { get; set; }
    Vector3 Position { get; }
    Rotation3 Orientation { get; set; }
    void Move(Vector3 translation);
    void PressButton(SimulatedSixDofControllerButton button);
    void ReleaseButton(SimulatedSixDofControllerButton button);
    void GetTouchpadPosition(out float x, out float y);
    void SetTouchpadPosition(float x, float y);
}
```

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. WorldPosition**

Récupérer la position du nœud par rapport au monde, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Status**

Récupère ou définit l’état actuel du contrôleur.  L’état du contrôleur doit être défini sur une valeur autre que OFF avant que les appels au déplacement, à la rotation ou à l’appui sur les boutons échouent.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. position**

Récupérez ou définissez la position du contrôleur simulé par rapport à l’homme, en mètres.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. orientation**

Récupérer ou définir l’orientation du contrôleur simulé.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Move (Microsoft. PerceptionSimulation. Vector3)**

Déplacer la position du contrôleur simulé par rapport à sa position actuelle, en mètres.

Paramètres
* Traduction : quantité de conversion du contrôleur simulé.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. PressButton (SimulatedSixDofControllerButton)**

Appuyez sur un bouton sur le contrôleur simulé.  Il ne sera détecté par le système que si le contrôleur est activé.

Paramètres
* Button-bouton sur lequel appuyer.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. ReleaseButton (SimulatedSixDofControllerButton)**

Publiez un bouton sur le contrôleur simulé.  Il ne sera détecté par le système que si le contrôleur est activé.

Paramètres
* Button-bouton à libérer.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. GetTouchpadPosition (sortie float, out float)**

Obtient la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.

Paramètres
* x-la position horizontale du doigt.
* y : position verticale du doigt.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController. SetTouchpadPosition (float, float)**

Définit la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.

Paramètres
* x-la position horizontale du doigt.
* y : position verticale du doigt.

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a>Microsoft. PerceptionSimulation. ISimulatedSixDofController2

Des propriétés et méthodes supplémentaires sont disponibles en convertissant un ISimulatedSixDofController en ISimulatedSixDofController2

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. GetThumbstickPosition (sortie float, out float)**

Obtient la position du stick analogique simulé sur le contrôleur simulé.

Paramètres
* x-la position horizontale du stick analogique.
* y : position verticale du stick analogique.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. SetThumbstickPosition (float, float)**

Définissez la position du stick analogique simulé sur le contrôleur simulé.

Paramètres
* x-la position horizontale du stick analogique.
* y : position verticale du stick analogique.

**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. BatteryLevel**

Récupérez ou définissez le niveau de batterie du contrôleur simulé.  La valeur doit être supérieure à 0,0 et inférieure ou égale à 100,0.


### <a name="microsoftperceptionsimulationisimulatedeyes"></a>Microsoft. PerceptionSimulation. ISimulatedEyes

Interface décrivant les yeux de l’homme simulé.

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

**Microsoft. PerceptionSimulation. ISimulatedEyes. rotation**

Récupérer la rotation des yeux simulés. Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.

**Microsoft. PerceptionSimulation. ISimulatedEyes. Rotate (Microsoft. PerceptionSimulation. Rotation3)**

Faire pivoter les yeux simulés par rapport à sa rotation actuelle. Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.

Paramètres
* rotation : quantité à faire pivoter.

**Microsoft. PerceptionSimulation. ISimulatedEyes. CalibrationState**

Récupère ou définit l’état d’étalonnage des yeux simulés.

**Microsoft. PerceptionSimulation. ISimulatedEyes. WorldPosition**

Récupérer la position du nœud par rapport au monde, en mètres.


### <a name="microsoftperceptionsimulationisimulationrecording"></a>Microsoft. PerceptionSimulation. ISimulationRecording

Interface pour l’interaction avec un enregistrement unique chargé pour la lecture.

```
public interface ISimulationRecording
{
    StreamDataTypes DataTypes { get; }
    PlaybackState State { get; }
    void Play();
    void Pause();
    void Seek(UInt64 ticks);
    void Stop();
};
```

**Microsoft. PerceptionSimulation. ISimulationRecording. DataTypes**

Récupère la liste des types de données dans l’enregistrement.

**Microsoft. PerceptionSimulation. ISimulationRecording. State**

Récupère l’état actuel de l’enregistrement.

**Microsoft. PerceptionSimulation. ISimulationRecording. Play**

Démarrez la lecture. Si l’enregistrement est suspendu, la lecture reprendra à partir de l’emplacement suspendu ; s’il est arrêté, la lecture démarre au début. Si elle est déjà en cours d’exécution, cet appel est ignoré.

**Microsoft. PerceptionSimulation. ISimulationRecording. pause**

Suspend la lecture à son emplacement actuel. Si l’enregistrement est arrêté, l’appel est ignoré.

**Microsoft. PerceptionSimulation. ISimulationRecording. Seek (System. UInt64)**

Recherche l’enregistrement à l’heure spécifiée (dans les intervalles de 100 nanosecondes à partir du début) et s’interrompt à cet emplacement. Si l’heure est postérieure à la fin de l’enregistrement, elle est mise en pause au niveau de la dernière image.

Paramètres
* cycles : heure à laquelle effectuer la recherche.

**Microsoft. PerceptionSimulation. ISimulationRecording. Stop**

Arrête la lecture et réinitialise la position au début.

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a>Microsoft. PerceptionSimulation. ISimulationRecordingCallback

Interface pour la réception des modifications d’État pendant la lecture.

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

**Microsoft. PerceptionSimulation. ISimulationRecordingCallback. PlaybackStateChanged (Microsoft. PerceptionSimulation. PlaybackState)**

Appelé lorsque l’état de lecture d’un ISimulationRecording a changé.

Paramètres
* newState : nouvel état de l’enregistrement.

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a>Microsoft. PerceptionSimulation. PerceptionSimulationManager

Objet racine pour la création d’objets de simulation de perception.

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationManager (Microsoft. PerceptionSimulation. ISimulationStreamSink)**

Créez sur un objet pour générer des paquets simulés et les fournir au récepteur fourni.

Paramètres
* Sink : récepteur qui recevra tous les paquets générés.

Valeur renvoyée

Gestionnaire créé.

**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationRecording (System. String)**

Créez un récepteur qui stocke tous les paquets reçus dans un fichier au chemin d’accès spécifié.

Paramètres
* chemin d’accès : chemin d’accès du fichier à créer.

Valeur renvoyée

Récepteur créé.

**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory)**

Charge un enregistrement à partir du fichier spécifié.

Paramètres
* chemin d’accès : chemin d’accès du fichier à charger.
* Factory : fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.

Valeur renvoyée

Enregistrement chargé.

**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory, Microsoft. PerceptionSimulation. ISimulationRecordingCallback)**

Charge un enregistrement à partir du fichier spécifié.

Paramètres
* chemin d’accès : chemin d’accès du fichier à charger.
* Factory : fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.
* callback : rappel qui reçoit les mises à jour qui regradent l’état de l’enregistrement.

Valeur renvoyée

Enregistrement chargé.

### <a name="microsoftperceptionsimulationstreamdatatypes"></a>Microsoft. PerceptionSimulation. StreamDataTypes

Décrit les différents types de données de flux.

```
public enum StreamDataTypes
{
    None = 0x00,
    Head = 0x01,
    Hands = 0x02,
    SpatialMapping = 0x08,
    Calibration = 0x10,
    Environment = 0x20,
    All = None | Head | Hands | SpatialMapping | Calibration | Environment
}
```

**Microsoft. PerceptionSimulation. StreamDataTypes. None**

Valeur de sentinelle utilisée pour indiquer l’absence de type de données de flux.

**Microsoft. PerceptionSimulation. StreamDataTypes. Head**

Flux de données concernant la position et l’orientation de l’en-tête.

**Microsoft. PerceptionSimulation. StreamDataTypes. mains**

Flux de données concernant la position et les gestes des mains.

**Microsoft. PerceptionSimulation. StreamDataTypes. SpatialMapping**

Flux de données concernant le mappage spatial de l’environnement.

**Microsoft. PerceptionSimulation. StreamDataTypes. étalonnage**

Flux de données concernant l’étalonnage de l’appareil. Les paquets d’étalonnage sont acceptés uniquement par un système en mode distant.

**Microsoft. PerceptionSimulation. StreamDataTypes. Environment**

Flux de données concernant l’environnement de l’appareil.

**Microsoft. PerceptionSimulation. StreamDataTypes. All**

Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrés.

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a>Microsoft. PerceptionSimulation. ISimulationStreamSink

Objet qui reçoit les paquets de données d’un flux de simulation.

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

**Microsoft. PerceptionSimulation. ISimulationStreamSink. OnPacketReceived (uint Length, Byte [] paquet)**

Reçoit un paquet unique, qui est typé en interne et avec version.

Paramètres
* Length-Longueur du paquet.
* paquet : données du paquet.

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a>Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory

Objet qui crée ISimulationStreamSink.

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

**Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory. CreateSimulationStreamSink ()**

Crée une seule instance de ISimulationStreamSink.

Valeur renvoyée

Récepteur créé.
