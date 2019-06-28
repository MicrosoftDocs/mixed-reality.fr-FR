---
title: Simulation de perception
description: Un guide d’utilisation de la bibliothèque de Simulation de Perception pour automatiser l’entrée simulée pour des applications immersives
author: pbarnettms
ms.author: pbarnett
ms.date: 04/26/2019
ms.topic: article
keywords: HoloLens, simulation, test
ms.openlocfilehash: 8152181bdbe8c83d2b706b34f1f2fb5d51f4c880
ms.sourcegitcommit: d8700260f349a09c53948e519bd6d8ed6f9bc4b4
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67414533"
---
# <a name="perception-simulation"></a>Simulation de perception

Vous souhaitez générer un test automatisé pour votre application ? Voulez-vous que vos tests d’aller au-delà des tests d’unités au niveau du composant et de véritablement tester votre application end-to-end ? Simulation de perception est ce que vous cherchez. La bibliothèque de Simulation de Perception envoie humaine et world les données d’entrée à votre application afin d’automatiser vos tests. Par exemple, vous pouvez simuler l’entrée d’un humain cherche à une position spécifique, reproductible et puis en effectuant un mouvement ou à l’aide d’un contrôleur de mouvement.

Simulation de perception peut envoyer simulée entrée comme ceci à un HoloLens physique, l’émulateur de HoloLens (1er gen), le HoloLens 2 émulateur ou un PC avec le portail de réalité mixte installé. Perception Simulation ignore les capteurs en direct sur un appareil de réalité mixte et envoie simulés entrée aux applications s’exécutant sur l’appareil. Les applications reçoivent ces événements d’entrée via les mêmes API qu’ils utilisent toujours et que vous ne pouvez pas faire la différence entre l’exécution avec des capteurs réels et l’exécution avec Simulation de Perception. Simulation de perception est la technologie utilisée par les émulateurs de HoloLens d’envoyer l’entrée simulée à la Machine virtuelle HoloLens.

Pour commencer à l’aide de la simulation dans votre code, commencez par créer un objet IPerceptionSimulationManager. À partir de cet objet, vous pouvez émettre des commandes permettant de contrôler les propriétés d’un simulé « humaine », y compris la position de tête, la position de la main et mouvements, et vous pouvez activer et manipuler des contrôleurs de mouvement.

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a>Configuration d’un projet Visual Studio pour la Simulation de Perception
1. [Installer l’émulateur de HoloLens](install-the-tools.md) sur votre PC de développement. L’émulateur inclut les bibliothèques que vous allez utiliser pour la Simulation de Perception.
2. Créer un nouveau Visual Studio C# projet de bureau (un projet Console fonctionne très bien prise en main).
3. Ajouter les fichiers binaires suivants à votre projet en tant que références (projet -> Ajouter -> référence...). Vous pouvez les trouver dans % ProgramFiles% (x86) %\Microsoft XDE\\(version), tel que **% ProgramFiles (x86) %\Microsoft XDE\\10.0.18362.0** pour l’émulateur de 2 HoloLens.  (Remarque : bien que les fichiers binaires font partie de l’émulateur de 2 HoloLens, ils fonctionnent également pour la réalité mixte Windows sur le bureau.) une barre d’outils. PerceptionSimulationManager.Interop.dll - managé C# wrapper pour la Simulation de Perception.
    b. PerceptionSimulationRest.dll - bibliothèque de configuration d’un canal de communication de socket web à l’HoloLens ou l’émulateur.
    c. SimulationStream.Interop.dll - types partagés pour la simulation.
4. Ajoutez l’implémentation PerceptionSimulationManager.dll binaire à votre projet une. Tout d’abord l’ajouter sous forme binaire au projet (projet -> Ajouter -> élément existant...). Enregistrez-le sous forme de lien afin qu’il ne le copie vers votre dossier source du projet. ![Ajouter au projet sous forme de lien PerceptionSimulationManager.dll](images/saveaslink.png) b. Assurez-vous qu’il le copié dans votre dossier de sortie sur la build. Il s’agit de la feuille de propriétés pour le fichier binaire. ![Marquer PerceptionSimulationManager.dll pour copier vers le répertoire de sortie](images/copyalways.png)
5. Définissez votre plateforme de solution active x64.  (Utilisez le Gestionnaire de Configuration pour créer une entrée de plateforme pour x64 s’il n’existe pas déjà).

## <a name="creating-an-iperceptionsimulation-manager-object"></a>Création d’un objet de gestionnaire IPerceptionSimulation

Pour contrôler la simulation, vous allez émettre des mises à jour pour les objets récupérés à partir d’un objet IPerceptionSimulationManager. La première étape consiste à obtenir cet objet et le connecter à votre appareil cible ou un émulateur. Vous pouvez obtenir l’adresse IP de votre émulateur en cliquant sur le bouton de portail de l’appareil dans le [barre d’outils](using-the-hololens-emulator.md)

![Icône d’ouverture de portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.  Pour la réalité mixte Windows, il peut être récupéré dans l’application de paramètres sous « Mise à jour et sécurité », puis « pour les développeurs » dans le « se connecter à l’aide de : « section sous « Portail de l’appareil Enable ».  Veillez à noter l’adresse IP et le port.

Tout d’abord, vous devez appeler RestSimulationStreamSink.Create pour obtenir un objet RestSimulationStreamSink. Il s’agit le périphérique cible ou l’émulateur qui contrôle via une connexion http. Vos commandes seront passés à et gérés par le [Windows Device Portal](using-the-windows-device-portal.md) en cours d’exécution sur le périphérique ou l’émulateur. Les quatre paramètres que vous aurez besoin pour créer un objet sont :
* Uri de l’URI : adresse IP de l’appareil cible (par exemple, « http://123.123.123.123 « ou » http://123.123.123.123:50080 »)
* Informations d’identification System.Net.NetworkCredential - nom d’utilisateur/mot de passe pour se connecter à la [Windows Device Portal](using-the-windows-device-portal.md) sur l’appareil cible ou l’émulateur. Si vous vous connectez à l’émulateur par le biais de son adresse locale (par exemple, 168. *.* . *) sur le même ordinateur, les informations d’identification seront acceptées.
* bool normal - True pour une priorité normale, false pour une priorité basse. Vous souhaitez généralement définir cela *true* pour les scénarios de test, ce qui permet à votre test afin de prendre le contrôle.  L’émulateur et la simulation de réalité mixte Windows utilisent des connexions de basse priorité.  Si votre test utilise également une connexion de faible priorité, le plus récemment été établie connexion sera dans le contrôle.
* Jeton System.Threading.CancellationToken - jeton pour annuler l’opération asynchrone.

Ensuite, vous allez créer le IPerceptionSimulationManager. Il s’agit de l’objet que vous utilisez pour contrôler la simulation. Notez que cela doit également être effectuée dans une méthode async.

## <a name="control-the-simulated-human"></a>Contrôle l’être humain simulé

Un IPerceptionSimulationManager a une propriété humain qui retourne un objet ISimulatedHuman. Pour contrôler l’être humain simulé, effectuer des opérations sur cet objet. Exemple :

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a>Exemple de base C# application console

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
                        new Uri("http://169.254.227.115"),
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

## <a name="extended-sample-c-console-application"></a>Étendue exemple C# application console

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
                        new Uri("http://169.254.227.115"),
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

## <a name="note-on-6-dof-controllers"></a>Remarque sur les contrôleurs de 6-DDL

Avant d’appeler toutes les propriétés sur les méthodes sur un contrôleur de 6-DDL simulé, vous devez activer le contrôleur.  Contraire, cela entraîne une exception.  À compter de Windows 10 peut 2019 mise à jour, les contrôleurs simulé 6-DDL peuvent être installés et activés en définissant la propriété d’état sur l’objet ISimulatedSixDofController à SimulatedSixDofControllerStatus.Active.
Dans les fenêtres de 10 octobre 2018 mettre à jour et versions antérieures, vous devez installer séparément un contrôleur simulé 6-DDL tout d’abord en appelant l’outil PerceptionSimulationDevice situé dans le dossier \Windows\System32.  L’utilisation de cet outil est la suivante :


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

Exemple :

```
    PerceptionSimulationDevice.exe i 6dof 1
```

Actions prises en charge sont :
* J’ai = install
* q = query
* r = supprimer

Les instances prises en charge sont :
* 1 = le contrôleur 6-DDL gauche
* 2 = le contrôleur 6-DDL droite

Indique le code de sortie du processus de réussite (valeur de retour de zéro) ou l’échec (une valeur de retour différente de zéro).  Lorsque vous utilisez l’action « q » pour interroger ou non un contrôleur est installé, la valeur de retour sera égal à zéro (0) si le contrôleur n’est pas déjà installé ou un (1) si le contrôleur est installé.

Lors de la suppression d’un contrôleur sur les fenêtres de mise à jour 10 octobre 2018 ou antérieures, définissez son état à désactiver via l’API tout d’abord, puis appelez l’outil PerceptionSimulationDevice.

Notez que cet outil doit être exécuté en tant qu’administrateur.




## <a name="api-reference"></a>Référence de l’API

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a>Microsoft.PerceptionSimulation.SimulatedDeviceType

Décrit un type d’appareil simulé

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**

Un appareil de référence fictive, la valeur par défaut pour PerceptionSimulationManager

### <a name="microsoftperceptionsimulationheadtrackermode"></a>Microsoft.PerceptionSimulation.HeadTrackerMode

Décrit un mode de suivi de la tête

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**

Valeur par défaut de la tête de suivi. Cela signifie que le système peut sélectionner la tête meilleures mode en fonction de conditions de runtime de suivi.

**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**

Orientation principaux uniquement le suivi. Cela signifie que la position de suivi n’est peut-être pas fiable, et certaines fonctionnalités qui dépendent de la position principale n’est peut-être pas disponible.

**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**

Suivi de la tête positionnels. Cela signifie que la position de tête suivie et l’orientation sont fiables

### <a name="microsoftperceptionsimulationsimulatedgesture"></a>Microsoft.PerceptionSimulation.SimulatedGesture

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

**Microsoft.PerceptionSimulation.SimulatedGesture.None**

Valeur de sentinelle permettant de n’indiquer aucune mouvements.

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**

Un doigt enfoncé mouvement.

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**

Un mouvement du doigt publié.

**Microsoft.PerceptionSimulation.SimulatedGesture.Home**

Le mouvement accueil/système.

**Microsoft.PerceptionSimulation.SimulatedGesture.Max**

Le mouvement valid maximal.

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a>Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus

Les états possibles d’un contrôleur de 6-DDL simulé.

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Off**

Le contrôleur de 6-DDL est désactivé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Active**

Le contrôleur de 6-DDL est activé et suivi.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.TrackingLost**

Le contrôleur de 6-DDL est activé, mais ne peut pas être suivi.

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a>Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton

Boutons de la prise en charge sur un contrôleur de 6-DDL simulé.

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

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.None**

Valeur de sentinelle permettant de n’indiquer aucun bouton.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Home**

Le bouton d’accueil est enfoncé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Menu**

Le bouton de Menu est activé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Grip**

La poignée de bouton est enfoncée.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadPress**

Le pavé tactile est enfoncé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Select**

Le bouton Sélectionner est enfoncé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadTouch**

Le pavé tactile est touché.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Thumbstick**

Le stick analogique est enfoncé.

**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Max**

Le bouton maximum valid.


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a>Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState

L’état de l’étalonnage des yeux simulés

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Unavailable**

L’étalonnage yeux n’est pas disponible.

**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Ready**

Les yeux ont été étalonnés.  Valeur par défaut.

**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**

Les yeux sont en cours d’étalonnage.

**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.UserCalibrationNeeded**

Les yeux ont besoin d’être étalonné.

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a>Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy

La précision de suivi d’un joint de la main.

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Unavailable**

La jointure n’est pas suivie.

**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Approximate**

La position commune est déduite.

**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Visible**

La jointure est entièrement suivie.

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a>Microsoft.PerceptionSimulation.SimulatedHandPose

La précision de suivi d’un joint de la main.

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

**Microsoft.PerceptionSimulation.SimulatedHandPose.Closed**

ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose fermée.

**Microsoft.PerceptionSimulation.SimulatedHandPose.Open**

Joints du doigt de l’aiguille sont configurés pour refléter une pose ouvert.

**Microsoft.PerceptionSimulation.SimulatedHandPose.Point**

ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose de pointage.

**Microsoft.PerceptionSimulation.SimulatedHandPose.Pinch**

ARTICULATIONS du doigt de l’aiguille sont configurées pour refléter une pose pincement.

**Microsoft.PerceptionSimulation.SimulatedHandPose.Max**

La valeur maximale valide pour SimulatedHandPose.


### <a name="microsoftperceptionsimulationplaybackstate"></a>Microsoft.PerceptionSimulation.PlaybackState

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

**Microsoft.PerceptionSimulation.PlaybackState.Stopped**

L’enregistrement est actuellement arrêté et prêt pour la lecture.

**Microsoft.PerceptionSimulation.PlaybackState.Playing**

L’enregistrement en cours de lecture.

**Microsoft.PerceptionSimulation.PlaybackState.Paused**

L’enregistrement est actuellement suspendu.

**Microsoft.PerceptionSimulation.PlaybackState.End**

L’enregistrement a atteint la fin.

### <a name="microsoftperceptionsimulationvector3"></a>Microsoft.PerceptionSimulation.Vector3

Décrit un vecteur de 3 composants, ce qui peut décrire un point ou un vecteur dans l’espace 3D.

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

**Microsoft.PerceptionSimulation.Vector3.X**

Le composant X du vecteur.

**Microsoft.PerceptionSimulation.Vector3.Y**

Le composant Y du vecteur.

**Microsoft.PerceptionSimulation.Vector3.Z**

Le composant Z du vecteur.

**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**

Construire un nouveau Vector3.

Paramètres
* x - composant x du vecteur.
* y - composant y du vecteur.
* z - composant z du vecteur.

### <a name="microsoftperceptionsimulationrotation3"></a>Microsoft.PerceptionSimulation.Rotation3

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

**Microsoft.PerceptionSimulation.Rotation3.Pitch**

Le composant de hauteur de la Rotation, vers le bas autour de l’axe X.

**Microsoft.PerceptionSimulation.Rotation3.Yaw**

Le composant lacet de Rotation vers la droite autour de l’axe Y.

**Microsoft.PerceptionSimulation.Rotation3.Roll**

Le composant de la restauration de la Rotation autour de l’axe Z.

**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**

Construire un nouveau Rotation3.

Paramètres
* pitch - le composant de hauteur de la Rotation.
* lacet - le composant lacet de la Rotation.
* restauration - le composant de restauration de la Rotation.

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a>Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration

Décrit la configuration d’un joint d’une part simulé.

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Position**

La position de la jointure.

**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Rotation**

La rotation de la jointure.

**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.TrackingAccuracy**

La précision de suivi de la jointure.


### <a name="microsoftperceptionsimulationfrustum"></a>Microsoft.PerceptionSimulation.Frustum

Décrit un frustum vue, comme cela est généralement utilisé par un appareil photo.

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

**Microsoft.PerceptionSimulation.Frustum.Near**

La distance minimale qui est contenue dans le frustum.

**Microsoft.PerceptionSimulation.Frustum.Far**

La distance maximale qui est contenue dans le frustum.

**Microsoft.PerceptionSimulation.Frustum.FieldOfView**

Le champ de vision horizontal de la frustum, en radians (inférieur à PI).

**Microsoft.PerceptionSimulation.Frustum.AspectRatio**

Le ratio de champ de vision horizontal pour le champ de vision verticale.

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.IPerceptionSimulationManager

Racine pour générer les paquets permettent de contrôler un appareil.

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**

Récupérer l’objet de périphérique simulé qui interprète l’être humain simulé et le monde simulé.

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**

Récupérer l’objet qui contrôle l’être humain simulé.

**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**

Réinitialise la simulation à son état par défaut.

### <a name="microsoftperceptionsimulationisimulateddevice"></a>Microsoft.PerceptionSimulation.ISimulatedDevice

Interface décrivant l’appareil qui interprète le monde simulé et l’être humain simulé

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**

Récupérer la tête de la mise hors tension à partir de l’appareil simulé.

**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**

Récupérer le dispositif de suivi disponible à partir de l’appareil simulé.

**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**

Définissez les propriétés de l’appareil simulé pour correspondre au type de l’appareil fourni.

Paramètres
* type - le nouveau type d’appareil simulé

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a>Microsoft.PerceptionSimulation.ISimulatedHeadTracker

Interface décrivant la partie de l’appareil simulé qui assure le suivi de la tête de l’être humain simulé.

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**

Récupère et définit le mode de suivi de la tête actuel.

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a>Microsoft.PerceptionSimulation.ISimulatedHandTracker

Interface décrivant la partie de l’appareil simulé qui assure le suivi entre les mains de l’être humain simulé

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

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**

Récupérer la position du nœud en relation avec le monde entier, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**

Récupérer et définir la position du dispositif de suivi main simulé, par rapport au centre de la tête.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**

Récupérez et définissez le pas vers le bas du dispositif de suivi main simulé.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**

Récupérez et définissez si le frustum du dispositif de suivi main simulé est ignoré. Lorsque ignorées, deux mains sont toujours visibles. Lorsque ne pas ignorées (la valeur par défaut) mains affichent uniquement quand ils se trouvent dans le frustum du dispositif de suivi de main.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**

Récupérer et définir les propriétés de frustum permet de déterminer si les mains sont visibles au dispositif de suivi main simulé.

### <a name="microsoftperceptionsimulationisimulatedhuman"></a>Microsoft.PerceptionSimulation.ISimulatedHuman

Interface de niveau supérieur pour le contrôle de l’être humain simulé.

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

**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**

Récupérer et définir la position du nœud en relation avec le monde entier, en mètres. La position correspond à un point dans le centre de mètres près de l’être humain.

**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**

Récupérer et définir la direction des visages humains simulés dans le monde. visages de 0 radian vers le bas de l’axe Z négatif. Radians positif rotation dans le sens horaire sur l’axe des Y.

**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**

Récupérer et définir la hauteur de l’être humain simulé, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**

Récupérer la main gauche de l’être humain simulé.

**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**

Récupérer la partie droite de l’être humain simulé.

**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**

Récupérer la tête de l’être humain simulé.

**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**

Déplacer l’être humain simulé par rapport à sa position actuelle, en mètres.

Paramètres
* traduction - la traduction à déplacer, par rapport à la position actuelle.

**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**

Faire pivoter l’être humain simulé par rapport à sa direction actuelle, dans le sens horaire autour de l’axe Y

Paramètres
* radians - la quantité pour faire pivoter autour de l’axe Y.

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a>Microsoft.PerceptionSimulation.ISimulatedHuman2

Propriétés supplémentaires sont disponibles en effectuant un cast de la ISimulatedHuman à ISimulatedHuman2

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedHuman2.LeftController**

Récupérer le contrôleur gauche 6-DDL.

**Microsoft.PerceptionSimulation.ISimulatedHuman2.RightController**

Récupérer le contrôleur de droite 6-DDL.


### <a name="microsoftperceptionsimulationisimulatedhand"></a>Microsoft.PerceptionSimulation.ISimulatedHand

Interface décrivant une main de l’être humain simulé

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

**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**

Récupérer la position du nœud en relation avec le monde entier, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedHand.Position**

Récupérer et définir la position de la main simulée par rapport à l’être humain, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**

Récupérez et définissez la valeur indiquant si la main est actuellement activée.

**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**

Récupérer si la main est actuellement visible pour le SimulatedDevice (si elle est dans une position pour être détecté par le HandTracker).

**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**

Déplacer la main tel qu’il soit visible par le SimulatedDevice.

**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**

Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.

Paramètres
* traduction - quantité de laquelle translater la main simulée.

**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**

Effectuer un mouvement à l’aide de la main simulée.  Elle sera détectée par le système uniquement si la main est activée.

Paramètres
* mouvement - mouvement à effectuer.

### <a name="microsoftperceptionsimulationisimulatedhand2"></a>Microsoft.PerceptionSimulation.ISimulatedHand2

Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHand à ISimulatedHand2.
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedHand2.Orientation**

Récupérer ou définir la rotation de l’aiguille simulé.  Radians rotation horaire lors de la recherche sur l’axe positif.

### <a name="microsoftperceptionsimulationisimulatedhand3"></a>Microsoft.PerceptionSimulation.ISimulatedHand3

Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHand à ISimulatedHand3
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

**Microsoft.PerceptionSimulation.ISimulatedHand3.GetJointConfiguration**

Obtenir la configuration commune pour la liaison spécifiée.

**Microsoft.PerceptionSimulation.ISimulatedHand3.SetJointConfiguration**

Définissez la configuration commune pour la liaison spécifiée.

**Microsoft.PerceptionSimulation.ISimulatedHand3.SetHandPose**

Une pose connue avec un indicateur facultatif pour animer la valeur la main.  Remarque : animation n’obtiendriez pas articulations immédiatement refléter leurs configurations mixte finales.


### <a name="microsoftperceptionsimulationisimulatedhead"></a>Microsoft.PerceptionSimulation.ISimulatedHead

Interface décrivant la tête de l’être humain simulé.

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**

Récupérer la position du nœud en relation avec le monde entier, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**

Récupérer la rotation de la tête. Radians rotation horaire lors de la recherche sur l’axe positif.

**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**

Récupérer le diamètre de la tête simulé. Cette valeur est utilisée pour déterminer le centre de la tête (point de rotation).

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**

Faire pivoter la tête par rapport à sa rotation actuelle. Radians rotation horaire lors de la recherche sur l’axe positif.

Paramètres
* rotation - la quantité pour faire pivoter.

### <a name="microsoftperceptionsimulationisimulatedhead2"></a>Microsoft.PerceptionSimulation.ISimulatedHead2

Propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedHead à ISimulatedHead2

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedHead2.Eyes**

Récupérer les yeux de l’être humain simulé.

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a>Microsoft.PerceptionSimulation.ISimulatedSixDofController

Interface décrivant un contrôleur de 6-DDL associé à l’être humain simulé.

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

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.WorldPosition**

Récupérer la position du nœud en relation avec le monde entier, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Status**

Récupérer ou définir l’état actuel du contrôleur.  L’état du contrôleur doit être définie sur une valeur autre que hors tension avant tout appel à déplacer, faire pivoter ou appuyez sur boutons réussira.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Position**

Récupérer ou définir la position du contrôleur simulé par rapport à l’être humain, en mètres.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Orientation**

Récupérer ou définir l’orientation du contrôleur simulé.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Move(Microsoft.PerceptionSimulation.Vector3)**

Déplacer la position du contrôleur simulé par rapport à sa position actuelle, en mètres.

Paramètres
* traduction - quantité de laquelle translater le contrôleur simulé.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.PressButton(SimulatedSixDofControllerButton)**

Appuyez sur un bouton sur le contrôleur simulé.  Il est détecté par le système uniquement si le contrôleur est activé.

Paramètres
* bouton - appuyez sur le bouton.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.ReleaseButton(SimulatedSixDofControllerButton)**

Relâchez un bouton sur le contrôleur simulé.  Il est détecté par le système uniquement si le contrôleur est activé.

Paramètres
* bouton - le bouton de mise en production.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.GetTouchpadPosition(out float, out float)**

Obtient la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.

Paramètres
* x - la position horizontale du doigt.
* y - la position verticale du doigt.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController.SetTouchpadPosition(float, float)**

Définir la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.

Paramètres
* x - la position horizontale du doigt.
* y - la position verticale du doigt.

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a>Microsoft.PerceptionSimulation.ISimulatedSixDofController2

Méthodes et propriétés supplémentaires sont disponibles en effectuant un cast d’un ISimulatedSixDofController à ISimulatedSixDofController2

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.GetThumbstickPosition(out float, out float)**

Obtient la position du stick analogique simulé sur le contrôleur simulé.

Paramètres
* x - la position horizontale du stick analogique.
* y - la position verticale du stick analogique.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.SetThumbstickPosition(float, float)**

Positionnez le stick analogique simulé sur le contrôleur simulé.

Paramètres
* x - la position horizontale du stick analogique.
* y - la position verticale du stick analogique.

**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**

Récupérer ou définir le niveau de la batterie du contrôleur simulé.  La valeur doit être supérieure à 0,0 et inférieure ou égale à 100,0.


### <a name="microsoftperceptionsimulationisimulatedeyes"></a>Microsoft.PerceptionSimulation.ISimulatedEyes

Interface décrivant les yeux de l’être humain simulé.

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotation**

Récupérer la rotation des yeux simulés. Radians rotation horaire lors de la recherche sur l’axe positif.

**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotate(Microsoft.PerceptionSimulation.Rotation3)**

Faire pivoter les yeux simulés par rapport à sa rotation actuelle. Radians rotation horaire lors de la recherche sur l’axe positif.

Paramètres
* rotation - la quantité pour faire pivoter.

**Microsoft.PerceptionSimulation.ISimulatedEyes.CalibrationState**

Récupère ou définit l’état de l’étalonnage des yeux simulés.

**Microsoft.PerceptionSimulation.ISimulatedEyes.WorldPosition**

Récupérer la position du nœud en relation avec le monde entier, en mètres.


### <a name="microsoftperceptionsimulationisimulationrecording"></a>Microsoft.PerceptionSimulation.ISimulationRecording

Charger de l’interface permettant d’interagir avec un enregistrement unique pour la lecture.

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

**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**

Récupère la liste des types de données dans l’enregistrement.

**Microsoft.PerceptionSimulation.ISimulationRecording.State**

Récupère l’état actuel de l’enregistrement.

**Microsoft.PerceptionSimulation.ISimulationRecording.Play**

Démarrer la lecture. Si l’enregistrement est suspendue, la lecture reprend à partir de l’emplacement en pause ; Si arrêté, la lecture démarre au début. Si vous déjà des données, cet appel est ignoré.

**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**

Suspend la lecture de son emplacement actuel. Si l’enregistrement est arrêté, l’appel est ignoré.

**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**

Cherche de l’enregistrement à l’heure spécifiée (100 nanosecondes par intervalles d’à partir du début) et s’interrompt à cet emplacement. Si l’heure est après la fin de l’enregistrement, il est suspendu au niveau de la dernière image.

Paramètres
* graduations - l’heure à laquelle effectuer une recherche.

**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**

Arrête la lecture et réinitialise la position au début.

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a>Microsoft.PerceptionSimulation.ISimulationRecordingCallback

Interface pour la réception des modifications d’état pendant la lecture.

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**

Appelée lorsque l’état de la lecture d’un ISimulationRecording a changé.

Paramètres
* newState - le nouvel état de l’enregistrement.

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.PerceptionSimulationManager

Objet racine pour la création d’objets de Simulation de Perception.

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**

Créer pour l’objet pour générer des paquets simulés et leur remise sur le récepteur fourni.

Paramètres
* récepteur - récepteur qui recevra les paquets générés.

Valeur de retour

Le gestionnaire créé.

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**

Créer un récepteur qui stocke les paquets reçus tout dans un fichier sur le chemin d’accès spécifié.

Paramètres
* chemin d’accès - le chemin d’accès du fichier à créer.

Valeur de retour

Le récepteur créé.

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**

Charger un enregistrement à partir du fichier spécifié.

Paramètres
* chemin d’accès - le chemin d’accès du fichier à charger.
* Factory - il s’agit d’une fabrique utilisée par l’enregistrement pour la création d’un ISimulationStreamSink si nécessaire.

Valeur de retour

L’enregistrement chargé.

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording (System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory, Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**

Charger un enregistrement à partir du fichier spécifié.

Paramètres
* chemin d’accès - le chemin d’accès du fichier à charger.
* Factory - il s’agit d’une fabrique utilisée par l’enregistrement pour la création d’un ISimulationStreamSink si nécessaire.
* rappel - un rappel qui reçoit des mises à jour déclassement d’état de l’enregistrement.

Valeur de retour

L’enregistrement chargé.

### <a name="microsoftperceptionsimulationstreamdatatypes"></a>Microsoft.PerceptionSimulation.StreamDataTypes

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

**Microsoft.PerceptionSimulation.StreamDataTypes.None**

Valeur de sentinelle permettant de n’indiquer aucun type de données de flux de données.

**Microsoft.PerceptionSimulation.StreamDataTypes.Head**

Stream des données relatives à la position et l’orientation de la tête.

**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**

Stream de données sur la position et les mouvements de mains.

**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**

Stream de données concernant le mappage spatial de l’environnement.

**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**

Stream de données concernant l’étalonnage de l’appareil. Paquets d’étalonnage sont uniquement acceptées par un système en Mode distant.

**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**

Stream de données concernant l’environnement de l’appareil.

**Microsoft.PerceptionSimulation.StreamDataTypes.All**

Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrées.

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a>Microsoft.PerceptionSimulation.ISimulationStreamSink

Objet qui reçoit des paquets de données à partir d’un flux de données de simulation.

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**

Reçoit un paquet unique, qui est en interne typés et avec contrôle de version.

Paramètres
* Length - la longueur du paquet.
* paquet - les données du paquet.

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a>Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory

Objet qui crée ISimulationStreamSink.

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**

Crée une instance unique de ISimulationStreamSink.

Valeur de retour

Le récepteur créé.
