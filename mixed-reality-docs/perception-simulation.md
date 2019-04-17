---
title: Simulation de perception
description: Un guide d’utilisation de la bibliothèque de Simulation de Perception pour automatiser l’entrée simulée pour des applications immersives
author: JonMLyons
ms.author: jlyons
ms.date: 03/21/2018
ms.topic: article
keywords: HoloLens, simulation, test
ms.openlocfilehash: 693750eb753bd11cbe7d7cfb47e04f1a3506ca9a
ms.sourcegitcommit: 384b0087899cd835a3a965f75c6f6c607c9edd1b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59595375"
---
# <a name="perception-simulation"></a>Simulation de perception

Vous souhaitez générer un test automatisé pour votre application ? Voulez-vous que vos tests d’aller au-delà des tests d’unités au niveau du composant et de véritablement tester votre application end-to-end ? Simulation de perception est ce que vous cherchez. La bibliothèque de Simulation de Perception envoie faux humaines et les données d’entrée dans le monde à votre application afin d’automatiser vos tests. Par exemple, vous pouvez simuler l’entrée d’une recherche humaine gauche et droite et puis en effectuant un mouvement.

Simulation de perception peut envoyer simulée entrée comme ceci à un HoloLens physique, l’émulateur de HoloLens ou un PC avec le portail de réalité mixte installé. Perception Simulation ignore les capteurs en direct sur un appareil de réalité mixte et envoie simulés entrée aux applications s’exécutant sur l’appareil. Les applications reçoivent ces événements d’entrée factices via les mêmes API toujours utiliser, ils ne peuvent pas faire la différence entre l’exécution avec des capteurs réels et l’exécution avec Simulation de Perception. Simulation de perception est la technologie utilisée par l’émulateur de HoloLens d’envoyer l’entrée simulée à la Machine virtuelle HoloLens.

Simulation démarre en créant un objet IPerceptionSimulationManager. À partir de cet objet, vous pouvez émettre des commandes permettant de contrôler les propriétés d’un simulé « humaine », y compris la position de tête, la position de la main et mouvements.

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a>Configuration d’un projet Visual Studio pour la Simulation de Perception
1. [Installer l’émulateur de HoloLens](install-the-tools.md) sur votre PC de développement. L’émulateur inclut les bibliothèques que vous allez utiliser pour la Simulation de Perception.
2. Créer un nouveau Visual Studio C# projet de bureau (un projet Console fonctionne très bien prise en main).
3. Ajouter les fichiers binaires suivants à votre projet en tant que références (projet -> Ajouter -> référence...). Vous les trouverez dans **% ProgramFiles (x86) %\Microsoft XDE\10.0.11082.0** un. PerceptionSimulationManager.Interop.dll - managé C# wrapper pour la Simulation de Perception.
    b. PerceptionSimulationRest.dll - bibliothèque de configuration d’un canal de communication de socket web à l’HoloLens ou l’émulateur.
    c. SimulationStream.Interop.dll - types partagés pour la simulation.
4. Ajoutez l’implémentation PerceptionSimulationManager.dll binaire à votre projet une. Tout d’abord l’ajouter sous forme binaire au projet (projet -> Ajouter -> élément existant...). Enregistrez-le sous forme de lien afin qu’il ne le copie vers votre dossier source du projet. ![Ajouter au projet sous forme de lien PerceptionSimulationManager.dll](images/saveaslink.png) b. Assurez-vous qu’il le copié dans votre dossier de sortie sur la build. Il s’agit de la feuille de propriétés pour le fichier binaire. ![Marquer PerceptionSimulationManager.dll pour copier vers le répertoire de sortie](images/copyalways.png)

## <a name="creating-an-iperceptionsimulation-manager-object"></a>Création d’un objet de gestionnaire IPerceptionSimulation

Pour contrôler la simulation, vous allez émettre des mises à jour pour les objets récupérés à partir d’un objet IPerceptionSimulationManager. La première étape consiste à obtenir cet objet et le connecter à votre appareil cible ou un émulateur. Vous pouvez obtenir l’adresse IP de votre émulateur en cliquant sur le bouton de portail de l’appareil dans le [barre d’outils](using-the-hololens-emulator.md#anatomy-of-the-hololens-emulator)

![Icône d’ouverture de portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: Ouvrez le Windows Device Portal pour le système d’exploitation de HoloLens dans l’émulateur.

Tout d’abord, vous devez appeler RestSimulationStreamSink.Create pour obtenir un objet RestSimulationStreamSink. Il s’agit le périphérique cible ou l’émulateur qui contrôle via une connexion http. Vos commandes seront passés à et gérés par le [Windows Device Portal](using-the-windows-device-portal.md) en cours d’exécution sur le périphérique ou l’émulateur. Les quatre paramètres que vous aurez besoin pour créer un objet sont :
* Uri de l’URI : adresse IP de l’appareil cible (par exemple, « http://123.123.123.123»)
* Informations d’identification System.Net.NetworkCredential - nom d’utilisateur/mot de passe pour se connecter à la [Windows Device Portal](using-the-windows-device-portal.md) sur l’appareil cible ou l’émulateur. Si vous vous connectez à l’émulateur par le biais de son 168 local. *.* . * adresse sur le même ordinateur, les informations d’identification seront acceptées.
* bool normal - True pour une priorité normale, false pour une priorité basse. Vous souhaitez généralement définir cela *true* pour les scénarios de test.
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
                try
                {
                    RestSimulationStreamSink sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("http://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        new System.Threading.CancellationToken());

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);
                }
                catch (Exception e)
                {
                    Console.WriteLine(e);
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
            Task.Run(async () =>
            {
                try
                {
                    RestSimulationStreamSink sink = await RestSimulationStreamSink.Create(
                        // use the IP address for your device/emulator
                        new Uri("http://169.254.227.115"),
                        // no credentials are needed for the emulator
                        new System.Net.NetworkCredential("", ""),
                        // normal priorty
                        true,
                        // cancel token
                        new System.Threading.CancellationToken());

                    IPerceptionSimulationManager manager = PerceptionSimulationManager.CreatePerceptionSimulationManager(sink);

                    // Now, we'll simulate a sequence of actions.
                    // Sleeps in-between each action give time to the system
                    // to be able to properly react.
                    // This is just an example. A proper automated test should verify
                    // that the app has behaved correctly
                    // before proceeding to the next step, instead of using Sleeps.

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
        }
    }
}
```

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

Valeur de sentinelle permettant de n’indiquer aucune mouvements

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**

Un doigt enfoncé mouvement

**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**

Un mouvement du doigt publié

**Microsoft.PerceptionSimulation.SimulatedGesture.Home**

Le mouvement d’accueil

**Microsoft.PerceptionSimulation.SimulatedGesture.Max**

Le mouvement valid maximal

### <a name="microsoftperceptionsimulationplaybackstate"></a>Microsoft.PerceptionSimulation.PlaybackState

Décrit l’état d’une lecture

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

L’enregistrement est actuellement arrêté et prêt pour la lecture

**Microsoft.PerceptionSimulation.PlaybackState.Playing**

L’enregistrement en cours de lecture

**Microsoft.PerceptionSimulation.PlaybackState.Paused**

L’enregistrement est actuellement suspendue.

**Microsoft.PerceptionSimulation.PlaybackState.End**

L’enregistrement a atteint la fin

### <a name="microsoftperceptionsimulationvector3"></a>Microsoft.PerceptionSimulation.Vector3

Décrit un vecteur de 3 composants, ce qui peut décrire un point ou un vecteur dans un espace 3D

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

Le composant X du vecteur

**Microsoft.PerceptionSimulation.Vector3.Y**

Le composant Y du vecteur

**Microsoft.PerceptionSimulation.Vector3.Z**

Le composant Z du vecteur

**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**

Construire un nouveau Vector3

Paramètres
* x - composant x du vecteur
* y - composant y du vecteur
* z - composant z du vecteur

### <a name="microsoftperceptionsimulationrotation3"></a>Microsoft.PerceptionSimulation.Rotation3

Décrit une rotation de 3 composants

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

Le composant de hauteur de la Rotation, vers le bas autour de l’axe X

**Microsoft.PerceptionSimulation.Rotation3.Yaw**

Le composant lacet de Rotation vers la droite autour de l’axe Y

**Microsoft.PerceptionSimulation.Rotation3.Roll**

Le composant de restauration de la Rotation autour de l’axe Z

**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**

Construire un nouveau Rotation3

Paramètres
* pitch - le composant de hauteur de la Rotation
* lacet - le composant lacet de la Rotation
* restauration - le composant de restauration de la Rotation

### <a name="microsoftperceptionsimulationfrustum"></a>Microsoft.PerceptionSimulation.Frustum

Décrit un frustum vue, comme cela est généralement utilisé par un appareil photo

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

La distance minimale qui est contenue dans le frustum

**Microsoft.PerceptionSimulation.Frustum.Far**

La distance maximale qui est contenue dans le frustum

**Microsoft.PerceptionSimulation.Frustum.FieldOfView**

Le champ de vision horizontal de la frustum, en radians (inférieur à PI)

**Microsoft.PerceptionSimulation.Frustum.AspectRatio**

Le rapport de champ de vision horizontal pour le champ de vision verticale

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.IPerceptionSimulationManager

Racine pour générer les paquets permettent de contrôler un appareil

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

Interface décrivant la partie de l’appareil simulé qui assure le suivi de la tête de l’être humain simulé

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

Récupérer la position du nœud en relation avec le monde entier, en mètres

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**

Récupérer et définir la position du dispositif de suivi main simulé, par rapport au centre de la tête.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**

Récupérer et définir la tonalité vers le bas du dispositif de suivi main simulé

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**

Récupérez et définissez si le frustum du dispositif de suivi main simulé est ignoré. Lorsque ignorées, deux mains sont toujours visibles. Lorsque ne pas ignorées (la valeur par défaut) mains affichent uniquement quand ils se trouvent dans le frustum du dispositif de suivi de main.

**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**

Récupérer et définir les propriétés de frustum permet de déterminer si les mains sont visibles au dispositif de suivi main simulé.

### <a name="microsoftperceptionsimulationisimulatedhuman"></a>Microsoft.PerceptionSimulation.ISimulatedHuman

Interface de niveau supérieur pour le contrôle de l’être humain simulé

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

Récupérer et définir la hauteur de l’être humain simulé, en mètres

**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**

Récupérer la main gauche de l’être humain simulé

**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**

Récupérer la partie droite de l’être humain simulé

**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**

Récupérer la tête de l’être humain simulé

**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**

Déplacer l’être humain simulé par rapport à sa position actuelle, en mètres

Paramètres
* traduction - la traduction à déplacer, par rapport à la position actuelle

**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**

Faire pivoter l’être humain simulé par rapport à sa direction actuelle, dans le sens horaire autour de l’axe Y

Paramètres
* radians - la quantité pour faire pivoter autour de l’axe Y

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

Récupérer la position du nœud en relation avec le monde entier, en mètres

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
* traduction - quantité de laquelle translater la main simulée

**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**

Effectuer un mouvement à l’aide de la main simulée (il sera uniquement être détecté par le système si la main est activée).

Paramètres
* mouvement - mouvement à effectuer

### <a name="microsoftperceptionsimulationisimulatedhead"></a>Microsoft.PerceptionSimulation.ISimulatedHead

Interface décrivant la tête de l’être humain simulé

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

Récupérer la position du nœud en relation avec le monde entier, en mètres

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**

Récupérer la rotation de la tête. Radians rotation horaire lors de la recherche sur l’axe positif.

**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**

Récupérer le diamètre de la tête simulé. Cette valeur est utilisée pour déterminer le centre de la tête (point de rotation).

**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**

Faire pivoter la tête par rapport à sa rotation actuelle. Radians rotation horaire lors de la recherche sur l’axe positif.

Paramètres
* rotation - la quantité pour faire pivoter

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
* graduations - l’heure à laquelle effectuer une recherche

**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**

Arrête la lecture et réinitialise la position au début

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a>Microsoft.PerceptionSimulation.ISimulationRecordingCallback

Interface pour la réception des modifications d’état pendant la lecture

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**

Appelée lorsque l’état de la lecture d’un ISimulationRecording a changé

Paramètres
* newState - le nouvel état de l’enregistrement

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a>Microsoft.PerceptionSimulation.PerceptionSimulationManager

Objet racine pour la création d’objets de Simulation de Perception

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
* récepteur - le récepteur qui recevra toutes générées paquets

Valeur de retour

Le gestionnaire créé

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**

Créer un récepteur qui stocke les paquets reçus tout dans un fichier sur le chemin d’accès spécifié.

Paramètres
* chemin d’accès - le chemin d’accès du fichier à créer

Valeur de retour

Le récepteur créé

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**

Charger un enregistrement à partir du fichier spécifié

Paramètres
* chemin d’accès - le chemin d’accès du fichier à charger
* Factory - une fabrique permettant de créer un ISimulationStreamSink lorsque requis par l’enregistrement

Valeur de retour

L’enregistrement chargé

**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording (System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory, Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**

Charger un enregistrement à partir du fichier spécifié

Paramètres
* chemin d’accès - le chemin d’accès du fichier à charger
* Factory - une fabrique permettant de créer un ISimulationStreamSink lorsque requis par l’enregistrement
* rappel - un rappel qui reçoit des mises à jour déclassement d’état de l’enregistrement

Valeur de retour

L’enregistrement chargé

### <a name="microsoftperceptionsimulationstreamdatatypes"></a>Microsoft.PerceptionSimulation.StreamDataTypes

Décrit les différents types de données de flux

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

Valeur de sentinelle permettant de n’indiquer aucun type de données de flux de données

**Microsoft.PerceptionSimulation.StreamDataTypes.Head**

Stream des données relatives à la position et l’orientation de la tête

**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**

Stream de données sur la position et les mouvements de mains

**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**

Stream de données concernant le mappage spatial de l’environnement

**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**

Stream de données concernant l’étalonnage de l’appareil. Paquets d’étalonnage sont uniquement acceptées par un système en Mode distant.

**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**

Stream de données concernant l’environnement de l’appareil

**Microsoft.PerceptionSimulation.StreamDataTypes.All**

Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrées

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a>Microsoft.PerceptionSimulation.ISimulationStreamSink

Objet qui reçoit des paquets de données à partir d’un flux de données de simulation

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**

Reçoit un paquet unique, qui est en interne typés et avec contrôle de version

Paramètres
* Length - la longueur du paquet
* paquet - les données du paquet

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a>Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory

Un objet qui crée ISimulationStreamSink

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**

Crée une instance unique de ISimulationStreamSink

Valeur de retour

Le récepteur créé
