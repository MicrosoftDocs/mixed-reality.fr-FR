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
# <a name="perception-simulation"></a><span data-ttu-id="04dc0-104">Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="04dc0-104">Perception simulation</span></span>

<span data-ttu-id="04dc0-105">Vous souhaitez générer un test automatisé pour votre application ?</span><span class="sxs-lookup"><span data-stu-id="04dc0-105">Do you want to build an automated test for your app?</span></span> <span data-ttu-id="04dc0-106">Voulez-vous que vos tests d’aller au-delà des tests d’unités au niveau du composant et de véritablement tester votre application end-to-end ?</span><span class="sxs-lookup"><span data-stu-id="04dc0-106">Do you want your tests to go beyond component-level unit testing and really exercise your app end-to-end?</span></span> <span data-ttu-id="04dc0-107">Simulation de perception est ce que vous cherchez.</span><span class="sxs-lookup"><span data-stu-id="04dc0-107">Perception Simulation is what you're looking for.</span></span> <span data-ttu-id="04dc0-108">La bibliothèque de Simulation de Perception envoie faux humaines et les données d’entrée dans le monde à votre application afin d’automatiser vos tests.</span><span class="sxs-lookup"><span data-stu-id="04dc0-108">The Perception Simulation library sends fake human and world input data to your app so you can automate your tests.</span></span> <span data-ttu-id="04dc0-109">Par exemple, vous pouvez simuler l’entrée d’une recherche humaine gauche et droite et puis en effectuant un mouvement.</span><span class="sxs-lookup"><span data-stu-id="04dc0-109">For example, you can simulate the input of a human looking left and right and then performing a gesture.</span></span>

<span data-ttu-id="04dc0-110">Simulation de perception peut envoyer simulée entrée comme ceci à un HoloLens physique, l’émulateur de HoloLens ou un PC avec le portail de réalité mixte installé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-110">Perception Simulation can send simulated input like this to a physical HoloLens, the HoloLens emulator, or a PC with Mixed Reality Portal installed.</span></span> <span data-ttu-id="04dc0-111">Perception Simulation ignore les capteurs en direct sur un appareil de réalité mixte et envoie simulés entrée aux applications s’exécutant sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="04dc0-111">Perception Simulation bypasses the live sensors on a Mixed Reality device and sends simulated input to applications running on the device.</span></span> <span data-ttu-id="04dc0-112">Les applications reçoivent ces événements d’entrée factices via les mêmes API toujours utiliser, ils ne peuvent pas faire la différence entre l’exécution avec des capteurs réels et l’exécution avec Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="04dc0-112">Applications receive these fake input events through the same APIs they always use, and can't tell the difference between running with real sensors versus running with Perception Simulation.</span></span> <span data-ttu-id="04dc0-113">Simulation de perception est la technologie utilisée par l’émulateur de HoloLens d’envoyer l’entrée simulée à la Machine virtuelle HoloLens.</span><span class="sxs-lookup"><span data-stu-id="04dc0-113">Perception Simulation is the same technology used by the HoloLens emulator to send simulated input to the HoloLens Virtual Machine.</span></span>

<span data-ttu-id="04dc0-114">Simulation démarre en créant un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="04dc0-114">Simulation starts by creating an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="04dc0-115">À partir de cet objet, vous pouvez émettre des commandes permettant de contrôler les propriétés d’un simulé « humaine », y compris la position de tête, la position de la main et mouvements.</span><span class="sxs-lookup"><span data-stu-id="04dc0-115">From that object, you can issue commands to control properties of a simulated "human", including head position, hand position, and gestures.</span></span>

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a><span data-ttu-id="04dc0-116">Configuration d’un projet Visual Studio pour la Simulation de Perception</span><span class="sxs-lookup"><span data-stu-id="04dc0-116">Setting Up a Visual Studio Project for Perception Simulation</span></span>
1. <span data-ttu-id="04dc0-117">[Installer l’émulateur de HoloLens](install-the-tools.md) sur votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="04dc0-117">[Install the HoloLens emulator](install-the-tools.md) on your development PC.</span></span> <span data-ttu-id="04dc0-118">L’émulateur inclut les bibliothèques que vous allez utiliser pour la Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="04dc0-118">The emulator includes the libraries you will use for Perception Simulation.</span></span>
2. <span data-ttu-id="04dc0-119">Créer un nouveau Visual Studio C# projet de bureau (un projet Console fonctionne très bien prise en main).</span><span class="sxs-lookup"><span data-stu-id="04dc0-119">Create a new Visual Studio C# desktop project (a Console Project works great to get started).</span></span>
3. <span data-ttu-id="04dc0-120">Ajouter les fichiers binaires suivants à votre projet en tant que références (projet -> Ajouter -> référence...). Vous les trouverez dans **% ProgramFiles (x86) %\Microsoft XDE\10.0.11082.0** un.</span><span class="sxs-lookup"><span data-stu-id="04dc0-120">Add the following binaries to your project as references (Project->Add->Reference...). You can find them in **%ProgramFiles(x86)%\Microsoft XDE\10.0.11082.0** a.</span></span> <span data-ttu-id="04dc0-121">PerceptionSimulationManager.Interop.dll - managé C# wrapper pour la Simulation de Perception.</span><span class="sxs-lookup"><span data-stu-id="04dc0-121">PerceptionSimulationManager.Interop.dll - Managed C# wrapper for Perception Simulation.</span></span>
    <span data-ttu-id="04dc0-122">b.</span><span class="sxs-lookup"><span data-stu-id="04dc0-122">b.</span></span> <span data-ttu-id="04dc0-123">PerceptionSimulationRest.dll - bibliothèque de configuration d’un canal de communication de socket web à l’HoloLens ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="04dc0-123">PerceptionSimulationRest.dll - Library for setting up a web-socket communication channel to the HoloLens or emulator.</span></span>
    <span data-ttu-id="04dc0-124">c.</span><span class="sxs-lookup"><span data-stu-id="04dc0-124">c.</span></span> <span data-ttu-id="04dc0-125">SimulationStream.Interop.dll - types partagés pour la simulation.</span><span class="sxs-lookup"><span data-stu-id="04dc0-125">SimulationStream.Interop.dll - Shared types for simulation.</span></span>
4. <span data-ttu-id="04dc0-126">Ajoutez l’implémentation PerceptionSimulationManager.dll binaire à votre projet une.</span><span class="sxs-lookup"><span data-stu-id="04dc0-126">Add the implementation binary PerceptionSimulationManager.dll to your project a.</span></span> <span data-ttu-id="04dc0-127">Tout d’abord l’ajouter sous forme binaire au projet (projet -> Ajouter -> élément existant...). Enregistrez-le sous forme de lien afin qu’il ne le copie vers votre dossier source du projet.</span><span class="sxs-lookup"><span data-stu-id="04dc0-127">First add it as a binary to the project (Project->Add->Existing Item...). Save it as a link so that it doesn't copy it to your project source folder.</span></span> <span data-ttu-id="04dc0-128">![Ajouter au projet sous forme de lien PerceptionSimulationManager.dll](images/saveaslink.png) b.</span><span class="sxs-lookup"><span data-stu-id="04dc0-128">![Add PerceptionSimulationManager.dll to the project as a link](images/saveaslink.png) b.</span></span> <span data-ttu-id="04dc0-129">Assurez-vous qu’il le copié dans votre dossier de sortie sur la build.</span><span class="sxs-lookup"><span data-stu-id="04dc0-129">Then make sure that it get's copied to your output folder on build.</span></span> <span data-ttu-id="04dc0-130">Il s’agit de la feuille de propriétés pour le fichier binaire.</span><span class="sxs-lookup"><span data-stu-id="04dc0-130">This is in the property sheet for the binary .</span></span> <span data-ttu-id="04dc0-131">![Marquer PerceptionSimulationManager.dll pour copier vers le répertoire de sortie](images/copyalways.png)</span><span class="sxs-lookup"><span data-stu-id="04dc0-131">![Mark PerceptionSimulationManager.dll to copy to the output directory](images/copyalways.png)</span></span>

## <a name="creating-an-iperceptionsimulation-manager-object"></a><span data-ttu-id="04dc0-132">Création d’un objet de gestionnaire IPerceptionSimulation</span><span class="sxs-lookup"><span data-stu-id="04dc0-132">Creating an IPerceptionSimulation Manager Object</span></span>

<span data-ttu-id="04dc0-133">Pour contrôler la simulation, vous allez émettre des mises à jour pour les objets récupérés à partir d’un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="04dc0-133">To control simulation, you'll issue updates to objects retrieved from an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="04dc0-134">La première étape consiste à obtenir cet objet et le connecter à votre appareil cible ou un émulateur.</span><span class="sxs-lookup"><span data-stu-id="04dc0-134">The first step is to get that object and connect it to your target device or emulator.</span></span> <span data-ttu-id="04dc0-135">Vous pouvez obtenir l’adresse IP de votre émulateur en cliquant sur le bouton de portail de l’appareil dans le [barre d’outils](using-the-hololens-emulator.md#anatomy-of-the-hololens-emulator)</span><span class="sxs-lookup"><span data-stu-id="04dc0-135">You can get the IP address of your emulator by clicking on the Device Portal button in the [toolbar](using-the-hololens-emulator.md#anatomy-of-the-hololens-emulator)</span></span>

<span data-ttu-id="04dc0-136">![Icône d’ouverture de portail de l’appareil](images/emulator-deviceportal.png) **ouvrir le portail de périphérique**: Ouvrez le Windows Device Portal pour le système d’exploitation de HoloLens dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="04dc0-136">![Open Device Portal icon](images/emulator-deviceportal.png) **Open Device Portal**: Open the Windows Device Portal for the HoloLens OS in the emulator.</span></span>

<span data-ttu-id="04dc0-137">Tout d’abord, vous devez appeler RestSimulationStreamSink.Create pour obtenir un objet RestSimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="04dc0-137">First, you'll call RestSimulationStreamSink.Create to get a RestSimulationStreamSink object.</span></span> <span data-ttu-id="04dc0-138">Il s’agit le périphérique cible ou l’émulateur qui contrôle via une connexion http.</span><span class="sxs-lookup"><span data-stu-id="04dc0-138">This is the target device or emulator that you will control over an http connection.</span></span> <span data-ttu-id="04dc0-139">Vos commandes seront passés à et gérés par le [Windows Device Portal](using-the-windows-device-portal.md) en cours d’exécution sur le périphérique ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="04dc0-139">Your commands will be passed to and handled by the [Windows Device Portal](using-the-windows-device-portal.md) running on the device or emulator.</span></span> <span data-ttu-id="04dc0-140">Les quatre paramètres que vous aurez besoin pour créer un objet sont :</span><span class="sxs-lookup"><span data-stu-id="04dc0-140">The four parameters you'll need to create an object are:</span></span>
* <span data-ttu-id="04dc0-141">Uri de l’URI : adresse IP de l’appareil cible (par exemple, « http://123.123.123.123»)</span><span class="sxs-lookup"><span data-stu-id="04dc0-141">Uri uri - IP address of the target device (e.g., "http://123.123.123.123")</span></span>
* <span data-ttu-id="04dc0-142">Informations d’identification System.Net.NetworkCredential - nom d’utilisateur/mot de passe pour se connecter à la [Windows Device Portal](using-the-windows-device-portal.md) sur l’appareil cible ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="04dc0-142">System.Net.NetworkCredential credentials - Username/password for connecting to the [Windows Device Portal](using-the-windows-device-portal.md) on the target device or emulator.</span></span> <span data-ttu-id="04dc0-143">Si vous vous connectez à l’émulateur par le biais de son 168 local. *.* . \* adresse sur le même ordinateur, les informations d’identification seront acceptées.</span><span class="sxs-lookup"><span data-stu-id="04dc0-143">If you are connecting to the emulator via its local 168.*.*.\* address on the same PC, any credentials will be accepted.</span></span>
* <span data-ttu-id="04dc0-144">bool normal - True pour une priorité normale, false pour une priorité basse.</span><span class="sxs-lookup"><span data-stu-id="04dc0-144">bool normal - True for normal priority, false for low priority.</span></span> <span data-ttu-id="04dc0-145">Vous souhaitez généralement définir cela *true* pour les scénarios de test.</span><span class="sxs-lookup"><span data-stu-id="04dc0-145">You generally want to set this to *true* for test scenarios.</span></span>
* <span data-ttu-id="04dc0-146">Jeton System.Threading.CancellationToken - jeton pour annuler l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="04dc0-146">System.Threading.CancellationToken token - Token to cancel the async operation.</span></span>

<span data-ttu-id="04dc0-147">Ensuite, vous allez créer le IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="04dc0-147">Second you will create the IPerceptionSimulationManager.</span></span> <span data-ttu-id="04dc0-148">Il s’agit de l’objet que vous utilisez pour contrôler la simulation.</span><span class="sxs-lookup"><span data-stu-id="04dc0-148">This is the object you use to control simulation.</span></span> <span data-ttu-id="04dc0-149">Notez que cela doit également être effectuée dans une méthode async.</span><span class="sxs-lookup"><span data-stu-id="04dc0-149">Note that this must also be done in an async method.</span></span>

## <a name="control-the-simulated-human"></a><span data-ttu-id="04dc0-150">Contrôle l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-150">Control the simulated Human</span></span>

<span data-ttu-id="04dc0-151">Un IPerceptionSimulationManager a une propriété humain qui retourne un objet ISimulatedHuman.</span><span class="sxs-lookup"><span data-stu-id="04dc0-151">An IPerceptionSimulationManager has a Human property that returns an ISimulatedHuman object.</span></span> <span data-ttu-id="04dc0-152">Pour contrôler l’être humain simulé, effectuer des opérations sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="04dc0-152">To control the simulated human, perform operations on this object.</span></span> <span data-ttu-id="04dc0-153">Exemple :</span><span class="sxs-lookup"><span data-stu-id="04dc0-153">For example:</span></span>

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a><span data-ttu-id="04dc0-154">Exemple de base C# application console</span><span class="sxs-lookup"><span data-stu-id="04dc0-154">Basic Sample C# console application</span></span>

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

## <a name="extended-sample-c-console-application"></a><span data-ttu-id="04dc0-155">Étendue exemple C# application console</span><span class="sxs-lookup"><span data-stu-id="04dc0-155">Extended Sample C# console application</span></span>

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

## <a name="api-reference"></a><span data-ttu-id="04dc0-156">Référence de l’API</span><span class="sxs-lookup"><span data-stu-id="04dc0-156">API Reference</span></span>

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a><span data-ttu-id="04dc0-157">Microsoft.PerceptionSimulation.SimulatedDeviceType</span><span class="sxs-lookup"><span data-stu-id="04dc0-157">Microsoft.PerceptionSimulation.SimulatedDeviceType</span></span>

<span data-ttu-id="04dc0-158">Décrit un type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-158">Describes a simulated device type</span></span>

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

<span data-ttu-id="04dc0-159">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span><span class="sxs-lookup"><span data-stu-id="04dc0-159">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span></span>

<span data-ttu-id="04dc0-160">Un appareil de référence fictive, la valeur par défaut pour PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="04dc0-160">A fictitious reference device, the default for PerceptionSimulationManager</span></span>

### <a name="microsoftperceptionsimulationheadtrackermode"></a><span data-ttu-id="04dc0-161">Microsoft.PerceptionSimulation.HeadTrackerMode</span><span class="sxs-lookup"><span data-stu-id="04dc0-161">Microsoft.PerceptionSimulation.HeadTrackerMode</span></span>

<span data-ttu-id="04dc0-162">Décrit un mode de suivi de la tête</span><span class="sxs-lookup"><span data-stu-id="04dc0-162">Describes a head tracker mode</span></span>

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

<span data-ttu-id="04dc0-163">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span><span class="sxs-lookup"><span data-stu-id="04dc0-163">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span></span>

<span data-ttu-id="04dc0-164">Valeur par défaut de la tête de suivi.</span><span class="sxs-lookup"><span data-stu-id="04dc0-164">Default Head Tracking.</span></span> <span data-ttu-id="04dc0-165">Cela signifie que le système peut sélectionner la tête meilleures mode en fonction de conditions de runtime de suivi.</span><span class="sxs-lookup"><span data-stu-id="04dc0-165">This means the system may select the best head tracking mode based upon runtime conditions.</span></span>

<span data-ttu-id="04dc0-166">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span><span class="sxs-lookup"><span data-stu-id="04dc0-166">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span></span>

<span data-ttu-id="04dc0-167">Orientation principaux uniquement le suivi.</span><span class="sxs-lookup"><span data-stu-id="04dc0-167">Orientation Only Head Tracking.</span></span> <span data-ttu-id="04dc0-168">Cela signifie que la position de suivi n’est peut-être pas fiable, et certaines fonctionnalités qui dépendent de la position principale n’est peut-être pas disponible.</span><span class="sxs-lookup"><span data-stu-id="04dc0-168">This means that the tracked position may not be reliable, and some functionality dependent on head position may not be available.</span></span>

<span data-ttu-id="04dc0-169">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span><span class="sxs-lookup"><span data-stu-id="04dc0-169">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span></span>

<span data-ttu-id="04dc0-170">Suivi de la tête positionnels.</span><span class="sxs-lookup"><span data-stu-id="04dc0-170">Positional Head Tracking.</span></span> <span data-ttu-id="04dc0-171">Cela signifie que la position de tête suivie et l’orientation sont fiables</span><span class="sxs-lookup"><span data-stu-id="04dc0-171">This means that the tracked head position and orientation are both reliable</span></span>

### <a name="microsoftperceptionsimulationsimulatedgesture"></a><span data-ttu-id="04dc0-172">Microsoft.PerceptionSimulation.SimulatedGesture</span><span class="sxs-lookup"><span data-stu-id="04dc0-172">Microsoft.PerceptionSimulation.SimulatedGesture</span></span>

<span data-ttu-id="04dc0-173">Décrit un mouvement simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-173">Describes a simulated gesture</span></span>

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

<span data-ttu-id="04dc0-174">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span><span class="sxs-lookup"><span data-stu-id="04dc0-174">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span></span>

<span data-ttu-id="04dc0-175">Valeur de sentinelle permettant de n’indiquer aucune mouvements</span><span class="sxs-lookup"><span data-stu-id="04dc0-175">A sentinel value used to indicate no gestures</span></span>

<span data-ttu-id="04dc0-176">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span><span class="sxs-lookup"><span data-stu-id="04dc0-176">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span></span>

<span data-ttu-id="04dc0-177">Un doigt enfoncé mouvement</span><span class="sxs-lookup"><span data-stu-id="04dc0-177">A finger pressed gesture</span></span>

<span data-ttu-id="04dc0-178">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span><span class="sxs-lookup"><span data-stu-id="04dc0-178">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span></span>

<span data-ttu-id="04dc0-179">Un mouvement du doigt publié</span><span class="sxs-lookup"><span data-stu-id="04dc0-179">A finger released gesture</span></span>

<span data-ttu-id="04dc0-180">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span><span class="sxs-lookup"><span data-stu-id="04dc0-180">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span></span>

<span data-ttu-id="04dc0-181">Le mouvement d’accueil</span><span class="sxs-lookup"><span data-stu-id="04dc0-181">The home gesture</span></span>

<span data-ttu-id="04dc0-182">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span><span class="sxs-lookup"><span data-stu-id="04dc0-182">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span></span>

<span data-ttu-id="04dc0-183">Le mouvement valid maximal</span><span class="sxs-lookup"><span data-stu-id="04dc0-183">The maximum valid gesture</span></span>

### <a name="microsoftperceptionsimulationplaybackstate"></a><span data-ttu-id="04dc0-184">Microsoft.PerceptionSimulation.PlaybackState</span><span class="sxs-lookup"><span data-stu-id="04dc0-184">Microsoft.PerceptionSimulation.PlaybackState</span></span>

<span data-ttu-id="04dc0-185">Décrit l’état d’une lecture</span><span class="sxs-lookup"><span data-stu-id="04dc0-185">Describes the state of a playback</span></span>

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

<span data-ttu-id="04dc0-186">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span><span class="sxs-lookup"><span data-stu-id="04dc0-186">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span></span>

<span data-ttu-id="04dc0-187">L’enregistrement est actuellement arrêté et prêt pour la lecture</span><span class="sxs-lookup"><span data-stu-id="04dc0-187">The recording is currently stopped and ready for playback</span></span>

<span data-ttu-id="04dc0-188">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span><span class="sxs-lookup"><span data-stu-id="04dc0-188">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span></span>

<span data-ttu-id="04dc0-189">L’enregistrement en cours de lecture</span><span class="sxs-lookup"><span data-stu-id="04dc0-189">The recording is currently playing</span></span>

<span data-ttu-id="04dc0-190">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span><span class="sxs-lookup"><span data-stu-id="04dc0-190">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span></span>

<span data-ttu-id="04dc0-191">L’enregistrement est actuellement suspendue.</span><span class="sxs-lookup"><span data-stu-id="04dc0-191">The recording is currently paused</span></span>

<span data-ttu-id="04dc0-192">**Microsoft.PerceptionSimulation.PlaybackState.End**</span><span class="sxs-lookup"><span data-stu-id="04dc0-192">**Microsoft.PerceptionSimulation.PlaybackState.End**</span></span>

<span data-ttu-id="04dc0-193">L’enregistrement a atteint la fin</span><span class="sxs-lookup"><span data-stu-id="04dc0-193">The recording has reached the end</span></span>

### <a name="microsoftperceptionsimulationvector3"></a><span data-ttu-id="04dc0-194">Microsoft.PerceptionSimulation.Vector3</span><span class="sxs-lookup"><span data-stu-id="04dc0-194">Microsoft.PerceptionSimulation.Vector3</span></span>

<span data-ttu-id="04dc0-195">Décrit un vecteur de 3 composants, ce qui peut décrire un point ou un vecteur dans un espace 3D</span><span class="sxs-lookup"><span data-stu-id="04dc0-195">Describes a 3 components vector, which might describe a point or a vector in 3D space</span></span>

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

<span data-ttu-id="04dc0-196">**Microsoft.PerceptionSimulation.Vector3.X**</span><span class="sxs-lookup"><span data-stu-id="04dc0-196">**Microsoft.PerceptionSimulation.Vector3.X**</span></span>

<span data-ttu-id="04dc0-197">Le composant X du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-197">The X component of the vector</span></span>

<span data-ttu-id="04dc0-198">**Microsoft.PerceptionSimulation.Vector3.Y**</span><span class="sxs-lookup"><span data-stu-id="04dc0-198">**Microsoft.PerceptionSimulation.Vector3.Y**</span></span>

<span data-ttu-id="04dc0-199">Le composant Y du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-199">The Y component of the vector</span></span>

<span data-ttu-id="04dc0-200">**Microsoft.PerceptionSimulation.Vector3.Z**</span><span class="sxs-lookup"><span data-stu-id="04dc0-200">**Microsoft.PerceptionSimulation.Vector3.Z**</span></span>

<span data-ttu-id="04dc0-201">Le composant Z du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-201">The Z component of the vector</span></span>

<span data-ttu-id="04dc0-202">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-202">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="04dc0-203">Construire un nouveau Vector3</span><span class="sxs-lookup"><span data-stu-id="04dc0-203">Construct a new Vector3</span></span>

<span data-ttu-id="04dc0-204">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-204">Parameters</span></span>
* <span data-ttu-id="04dc0-205">x - composant x du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-205">x - The x component of the vector</span></span>
* <span data-ttu-id="04dc0-206">y - composant y du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-206">y - The y component of the vector</span></span>
* <span data-ttu-id="04dc0-207">z - composant z du vecteur</span><span class="sxs-lookup"><span data-stu-id="04dc0-207">z - The z component of the vector</span></span>

### <a name="microsoftperceptionsimulationrotation3"></a><span data-ttu-id="04dc0-208">Microsoft.PerceptionSimulation.Rotation3</span><span class="sxs-lookup"><span data-stu-id="04dc0-208">Microsoft.PerceptionSimulation.Rotation3</span></span>

<span data-ttu-id="04dc0-209">Décrit une rotation de 3 composants</span><span class="sxs-lookup"><span data-stu-id="04dc0-209">Describes a 3 components rotation</span></span>

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

<span data-ttu-id="04dc0-210">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span><span class="sxs-lookup"><span data-stu-id="04dc0-210">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span></span>

<span data-ttu-id="04dc0-211">Le composant de hauteur de la Rotation, vers le bas autour de l’axe X</span><span class="sxs-lookup"><span data-stu-id="04dc0-211">The Pitch component of the Rotation, down around the X axis</span></span>

<span data-ttu-id="04dc0-212">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span><span class="sxs-lookup"><span data-stu-id="04dc0-212">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span></span>

<span data-ttu-id="04dc0-213">Le composant lacet de Rotation vers la droite autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="04dc0-213">The Yaw component of the Rotation, right around the Y axis</span></span>

<span data-ttu-id="04dc0-214">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span><span class="sxs-lookup"><span data-stu-id="04dc0-214">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span></span>

<span data-ttu-id="04dc0-215">Le composant de restauration de la Rotation autour de l’axe Z</span><span class="sxs-lookup"><span data-stu-id="04dc0-215">The Roll component of the Rotation, right around the Z axis</span></span>

<span data-ttu-id="04dc0-216">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-216">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="04dc0-217">Construire un nouveau Rotation3</span><span class="sxs-lookup"><span data-stu-id="04dc0-217">Construct a new Rotation3</span></span>

<span data-ttu-id="04dc0-218">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-218">Parameters</span></span>
* <span data-ttu-id="04dc0-219">pitch - le composant de hauteur de la Rotation</span><span class="sxs-lookup"><span data-stu-id="04dc0-219">pitch - The pitch component of the Rotation</span></span>
* <span data-ttu-id="04dc0-220">lacet - le composant lacet de la Rotation</span><span class="sxs-lookup"><span data-stu-id="04dc0-220">yaw - The yaw component of the Rotation</span></span>
* <span data-ttu-id="04dc0-221">restauration - le composant de restauration de la Rotation</span><span class="sxs-lookup"><span data-stu-id="04dc0-221">roll - The roll component of the Rotation</span></span>

### <a name="microsoftperceptionsimulationfrustum"></a><span data-ttu-id="04dc0-222">Microsoft.PerceptionSimulation.Frustum</span><span class="sxs-lookup"><span data-stu-id="04dc0-222">Microsoft.PerceptionSimulation.Frustum</span></span>

<span data-ttu-id="04dc0-223">Décrit un frustum vue, comme cela est généralement utilisé par un appareil photo</span><span class="sxs-lookup"><span data-stu-id="04dc0-223">Describes a view frustum, as typically used by a camera</span></span>

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

<span data-ttu-id="04dc0-224">**Microsoft.PerceptionSimulation.Frustum.Near**</span><span class="sxs-lookup"><span data-stu-id="04dc0-224">**Microsoft.PerceptionSimulation.Frustum.Near**</span></span>

<span data-ttu-id="04dc0-225">La distance minimale qui est contenue dans le frustum</span><span class="sxs-lookup"><span data-stu-id="04dc0-225">The minimum distance that is contained in the frustum</span></span>

<span data-ttu-id="04dc0-226">**Microsoft.PerceptionSimulation.Frustum.Far**</span><span class="sxs-lookup"><span data-stu-id="04dc0-226">**Microsoft.PerceptionSimulation.Frustum.Far**</span></span>

<span data-ttu-id="04dc0-227">La distance maximale qui est contenue dans le frustum</span><span class="sxs-lookup"><span data-stu-id="04dc0-227">The maximum distance that is contained in the frustum</span></span>

<span data-ttu-id="04dc0-228">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span><span class="sxs-lookup"><span data-stu-id="04dc0-228">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span></span>

<span data-ttu-id="04dc0-229">Le champ de vision horizontal de la frustum, en radians (inférieur à PI)</span><span class="sxs-lookup"><span data-stu-id="04dc0-229">The horizontal field of view of the frustum, in radians (less than PI)</span></span>

<span data-ttu-id="04dc0-230">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span><span class="sxs-lookup"><span data-stu-id="04dc0-230">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span></span>

<span data-ttu-id="04dc0-231">Le rapport de champ de vision horizontal pour le champ de vision verticale</span><span class="sxs-lookup"><span data-stu-id="04dc0-231">The ratio of horizontal field of view to vertical field of view</span></span>

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a><span data-ttu-id="04dc0-232">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="04dc0-232">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span></span>

<span data-ttu-id="04dc0-233">Racine pour générer les paquets permettent de contrôler un appareil</span><span class="sxs-lookup"><span data-stu-id="04dc0-233">Root for generating the packets used to control a device</span></span>

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

<span data-ttu-id="04dc0-234">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span><span class="sxs-lookup"><span data-stu-id="04dc0-234">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span></span>

<span data-ttu-id="04dc0-235">Récupérer l’objet de périphérique simulé qui interprète l’être humain simulé et le monde simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-235">Retrieve the simulated device object that interprets the simulated human and the simulated world.</span></span>

<span data-ttu-id="04dc0-236">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span><span class="sxs-lookup"><span data-stu-id="04dc0-236">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span></span>

<span data-ttu-id="04dc0-237">Récupérer l’objet qui contrôle l’être humain simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-237">Retrieve the object that controls the simulated human.</span></span>

<span data-ttu-id="04dc0-238">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span><span class="sxs-lookup"><span data-stu-id="04dc0-238">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span></span>

<span data-ttu-id="04dc0-239">Réinitialise la simulation à son état par défaut.</span><span class="sxs-lookup"><span data-stu-id="04dc0-239">Resets the simulation to its default state.</span></span>

### <a name="microsoftperceptionsimulationisimulateddevice"></a><span data-ttu-id="04dc0-240">Microsoft.PerceptionSimulation.ISimulatedDevice</span><span class="sxs-lookup"><span data-stu-id="04dc0-240">Microsoft.PerceptionSimulation.ISimulatedDevice</span></span>

<span data-ttu-id="04dc0-241">Interface décrivant l’appareil qui interprète le monde simulé et l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-241">Interface describing the device which interprets the simulated world and the simulated human</span></span>

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

<span data-ttu-id="04dc0-242">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span><span class="sxs-lookup"><span data-stu-id="04dc0-242">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span></span>

<span data-ttu-id="04dc0-243">Récupérer la tête de la mise hors tension à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-243">Retrieve the Head Tracker from the Simulated Device.</span></span>

<span data-ttu-id="04dc0-244">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span><span class="sxs-lookup"><span data-stu-id="04dc0-244">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span></span>

<span data-ttu-id="04dc0-245">Récupérer le dispositif de suivi disponible à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-245">Retrieve the Hand Tracker from the Simulated Device.</span></span>

<span data-ttu-id="04dc0-246">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-246">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span></span>

<span data-ttu-id="04dc0-247">Définissez les propriétés de l’appareil simulé pour correspondre au type de l’appareil fourni.</span><span class="sxs-lookup"><span data-stu-id="04dc0-247">Set the properties of the simulated device to match the provided device type.</span></span>

<span data-ttu-id="04dc0-248">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-248">Parameters</span></span>
* <span data-ttu-id="04dc0-249">type - le nouveau type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-249">type - The new type of Simulated Device</span></span>

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a><span data-ttu-id="04dc0-250">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span><span class="sxs-lookup"><span data-stu-id="04dc0-250">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span></span>

<span data-ttu-id="04dc0-251">Interface décrivant la partie de l’appareil simulé qui assure le suivi de la tête de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-251">Interface describing the portion of the simulated device that tracks the head of the simulated human</span></span>

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

<span data-ttu-id="04dc0-252">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span><span class="sxs-lookup"><span data-stu-id="04dc0-252">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span></span>

<span data-ttu-id="04dc0-253">Récupère et définit le mode de suivi de la tête actuel.</span><span class="sxs-lookup"><span data-stu-id="04dc0-253">Retrieves and sets the current head tracker mode.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a><span data-ttu-id="04dc0-254">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span><span class="sxs-lookup"><span data-stu-id="04dc0-254">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span></span>

<span data-ttu-id="04dc0-255">Interface décrivant la partie de l’appareil simulé qui assure le suivi entre les mains de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-255">Interface describing the portion of the simulated device that tracks the hands of the simulated human</span></span>

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

<span data-ttu-id="04dc0-256">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="04dc0-256">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span></span>

<span data-ttu-id="04dc0-257">Récupérer la position du nœud en relation avec le monde entier, en mètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-257">Retrieve the position of the node with relation to the world, in meters</span></span>

<span data-ttu-id="04dc0-258">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span><span class="sxs-lookup"><span data-stu-id="04dc0-258">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span></span>

<span data-ttu-id="04dc0-259">Récupérer et définir la position du dispositif de suivi main simulé, par rapport au centre de la tête.</span><span class="sxs-lookup"><span data-stu-id="04dc0-259">Retrieve and set the position of the simulated hand tracker, relative to the center of the head.</span></span>

<span data-ttu-id="04dc0-260">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span><span class="sxs-lookup"><span data-stu-id="04dc0-260">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span></span>

<span data-ttu-id="04dc0-261">Récupérer et définir la tonalité vers le bas du dispositif de suivi main simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-261">Retrieve and set the downward pitch of the simulated hand tracker</span></span>

<span data-ttu-id="04dc0-262">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span><span class="sxs-lookup"><span data-stu-id="04dc0-262">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span></span>

<span data-ttu-id="04dc0-263">Récupérez et définissez si le frustum du dispositif de suivi main simulé est ignoré.</span><span class="sxs-lookup"><span data-stu-id="04dc0-263">Retrieve and set whether the frustum of the simulated hand tracker is ignored.</span></span> <span data-ttu-id="04dc0-264">Lorsque ignorées, deux mains sont toujours visibles.</span><span class="sxs-lookup"><span data-stu-id="04dc0-264">When ignored, both hands are always visible.</span></span> <span data-ttu-id="04dc0-265">Lorsque ne pas ignorées (la valeur par défaut) mains affichent uniquement quand ils se trouvent dans le frustum du dispositif de suivi de main.</span><span class="sxs-lookup"><span data-stu-id="04dc0-265">When not ignored (the default) hands are only visible when they are within the frustum of the hand tracker.</span></span>

<span data-ttu-id="04dc0-266">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span><span class="sxs-lookup"><span data-stu-id="04dc0-266">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span></span>

<span data-ttu-id="04dc0-267">Récupérer et définir les propriétés de frustum permet de déterminer si les mains sont visibles au dispositif de suivi main simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-267">Retrieve and set the frustum properties used to determine if hands are visible to the simulated hand tracker.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman"></a><span data-ttu-id="04dc0-268">Microsoft.PerceptionSimulation.ISimulatedHuman</span><span class="sxs-lookup"><span data-stu-id="04dc0-268">Microsoft.PerceptionSimulation.ISimulatedHuman</span></span>

<span data-ttu-id="04dc0-269">Interface de niveau supérieur pour le contrôle de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-269">Top level interface for controlling the simulated human</span></span>

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

<span data-ttu-id="04dc0-270">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="04dc0-270">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span></span>

<span data-ttu-id="04dc0-271">Récupérer et définir la position du nœud en relation avec le monde entier, en mètres.</span><span class="sxs-lookup"><span data-stu-id="04dc0-271">Retrieve and set the position of the node with relation to the world, in meters.</span></span> <span data-ttu-id="04dc0-272">La position correspond à un point dans le centre de mètres près de l’être humain.</span><span class="sxs-lookup"><span data-stu-id="04dc0-272">The position corresponds to a point at the center of the human's feet.</span></span>

<span data-ttu-id="04dc0-273">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span><span class="sxs-lookup"><span data-stu-id="04dc0-273">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span></span>

<span data-ttu-id="04dc0-274">Récupérer et définir la direction des visages humains simulés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="04dc0-274">Retrieve and set the direction the simulated human faces in the world.</span></span> <span data-ttu-id="04dc0-275">visages de 0 radian vers le bas de l’axe Z négatif.</span><span class="sxs-lookup"><span data-stu-id="04dc0-275">0 radians faces down the negative Z axis.</span></span> <span data-ttu-id="04dc0-276">Radians positif rotation dans le sens horaire sur l’axe des Y.</span><span class="sxs-lookup"><span data-stu-id="04dc0-276">Positive radians rotate clockwise about the Y axis.</span></span>

<span data-ttu-id="04dc0-277">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span><span class="sxs-lookup"><span data-stu-id="04dc0-277">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span></span>

<span data-ttu-id="04dc0-278">Récupérer et définir la hauteur de l’être humain simulé, en mètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-278">Retrieve and set the height of the simulated human, in meters</span></span>

<span data-ttu-id="04dc0-279">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span><span class="sxs-lookup"><span data-stu-id="04dc0-279">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span></span>

<span data-ttu-id="04dc0-280">Récupérer la main gauche de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-280">Retrieve the left hand of the simulated human</span></span>

<span data-ttu-id="04dc0-281">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span><span class="sxs-lookup"><span data-stu-id="04dc0-281">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span></span>

<span data-ttu-id="04dc0-282">Récupérer la partie droite de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-282">Retrieve the right hand of the simulated human</span></span>

<span data-ttu-id="04dc0-283">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span><span class="sxs-lookup"><span data-stu-id="04dc0-283">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span></span>

<span data-ttu-id="04dc0-284">Récupérer la tête de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-284">Retrieve the head of the simulated human</span></span>

<span data-ttu-id="04dc0-285">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-285">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="04dc0-286">Déplacer l’être humain simulé par rapport à sa position actuelle, en mètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-286">Move the simulated human relative to its current position, in meters</span></span>

<span data-ttu-id="04dc0-287">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-287">Parameters</span></span>
* <span data-ttu-id="04dc0-288">traduction - la traduction à déplacer, par rapport à la position actuelle</span><span class="sxs-lookup"><span data-stu-id="04dc0-288">translation - The translation to move, relative to current position</span></span>

<span data-ttu-id="04dc0-289">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-289">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span></span>

<span data-ttu-id="04dc0-290">Faire pivoter l’être humain simulé par rapport à sa direction actuelle, dans le sens horaire autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="04dc0-290">Rotate the simulated human relative to its current direction, clockwise about the Y axis</span></span>

<span data-ttu-id="04dc0-291">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-291">Parameters</span></span>
* <span data-ttu-id="04dc0-292">radians - la quantité pour faire pivoter autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="04dc0-292">radians - The amount to rotate around the Y axis</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand"></a><span data-ttu-id="04dc0-293">Microsoft.PerceptionSimulation.ISimulatedHand</span><span class="sxs-lookup"><span data-stu-id="04dc0-293">Microsoft.PerceptionSimulation.ISimulatedHand</span></span>

<span data-ttu-id="04dc0-294">Interface décrivant une main de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-294">Interface describing a hand of the simulated human</span></span>

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

<span data-ttu-id="04dc0-295">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="04dc0-295">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span></span>

<span data-ttu-id="04dc0-296">Récupérer la position du nœud en relation avec le monde entier, en mètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-296">Retrieve the position of the node with relation to the world, in meters</span></span>

<span data-ttu-id="04dc0-297">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span><span class="sxs-lookup"><span data-stu-id="04dc0-297">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span></span>

<span data-ttu-id="04dc0-298">Récupérer et définir la position de la main simulée par rapport à l’être humain, en mètres.</span><span class="sxs-lookup"><span data-stu-id="04dc0-298">Retrieve and set the position of the simulated hand relative to the human, in meters.</span></span>

<span data-ttu-id="04dc0-299">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span><span class="sxs-lookup"><span data-stu-id="04dc0-299">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span></span>

<span data-ttu-id="04dc0-300">Récupérez et définissez la valeur indiquant si la main est actuellement activée.</span><span class="sxs-lookup"><span data-stu-id="04dc0-300">Retrieve and set whether the hand is currently activated.</span></span>

<span data-ttu-id="04dc0-301">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span><span class="sxs-lookup"><span data-stu-id="04dc0-301">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span></span>

<span data-ttu-id="04dc0-302">Récupérer si la main est actuellement visible pour le SimulatedDevice (si elle est dans une position pour être détecté par le HandTracker).</span><span class="sxs-lookup"><span data-stu-id="04dc0-302">Retrieve whether the hand is currently visible to the SimulatedDevice (ie, whether it's in a position to be detected by the HandTracker).</span></span>

<span data-ttu-id="04dc0-303">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span><span class="sxs-lookup"><span data-stu-id="04dc0-303">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span></span>

<span data-ttu-id="04dc0-304">Déplacer la main tel qu’il soit visible par le SimulatedDevice.</span><span class="sxs-lookup"><span data-stu-id="04dc0-304">Move the hand such that it is visible to the SimulatedDevice.</span></span>

<span data-ttu-id="04dc0-305">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-305">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="04dc0-306">Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="04dc0-306">Move the position of the simulated hand relative to its current position, in meters.</span></span>

<span data-ttu-id="04dc0-307">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-307">Parameters</span></span>
* <span data-ttu-id="04dc0-308">traduction - quantité de laquelle translater la main simulée</span><span class="sxs-lookup"><span data-stu-id="04dc0-308">translation - The amount to translate the simulated hand</span></span>

<span data-ttu-id="04dc0-309">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-309">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span></span>

<span data-ttu-id="04dc0-310">Effectuer un mouvement à l’aide de la main simulée (il sera uniquement être détecté par le système si la main est activée).</span><span class="sxs-lookup"><span data-stu-id="04dc0-310">Perform a gesture using the simulated hand (it will only be detected by the system if the hand is enabled).</span></span>

<span data-ttu-id="04dc0-311">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-311">Parameters</span></span>
* <span data-ttu-id="04dc0-312">mouvement - mouvement à effectuer</span><span class="sxs-lookup"><span data-stu-id="04dc0-312">gesture - The gesture to perform</span></span>

### <a name="microsoftperceptionsimulationisimulatedhead"></a><span data-ttu-id="04dc0-313">Microsoft.PerceptionSimulation.ISimulatedHead</span><span class="sxs-lookup"><span data-stu-id="04dc0-313">Microsoft.PerceptionSimulation.ISimulatedHead</span></span>

<span data-ttu-id="04dc0-314">Interface décrivant la tête de l’être humain simulé</span><span class="sxs-lookup"><span data-stu-id="04dc0-314">Interface describing the head of the simulated human</span></span>

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

<span data-ttu-id="04dc0-315">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="04dc0-315">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span></span>

<span data-ttu-id="04dc0-316">Récupérer la position du nœud en relation avec le monde entier, en mètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-316">Retrieve the position of the node with relation to the world, in meters</span></span>

<span data-ttu-id="04dc0-317">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span><span class="sxs-lookup"><span data-stu-id="04dc0-317">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span></span>

<span data-ttu-id="04dc0-318">Récupérer la rotation de la tête.</span><span class="sxs-lookup"><span data-stu-id="04dc0-318">Retrieve the rotation of the simulated head.</span></span> <span data-ttu-id="04dc0-319">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="04dc0-319">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="04dc0-320">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span><span class="sxs-lookup"><span data-stu-id="04dc0-320">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span></span>

<span data-ttu-id="04dc0-321">Récupérer le diamètre de la tête simulé.</span><span class="sxs-lookup"><span data-stu-id="04dc0-321">Retrieve the simulated head's diameter.</span></span> <span data-ttu-id="04dc0-322">Cette valeur est utilisée pour déterminer le centre de la tête (point de rotation).</span><span class="sxs-lookup"><span data-stu-id="04dc0-322">This value is used to determine the head's center (point of rotation).</span></span>

<span data-ttu-id="04dc0-323">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-323">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="04dc0-324">Faire pivoter la tête par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="04dc0-324">Rotate the simulated head relative to its current rotation.</span></span> <span data-ttu-id="04dc0-325">Radians rotation horaire lors de la recherche sur l’axe positif.</span><span class="sxs-lookup"><span data-stu-id="04dc0-325">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="04dc0-326">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-326">Parameters</span></span>
* <span data-ttu-id="04dc0-327">rotation - la quantité pour faire pivoter</span><span class="sxs-lookup"><span data-stu-id="04dc0-327">rotation - The amount to rotate</span></span>

### <a name="microsoftperceptionsimulationisimulationrecording"></a><span data-ttu-id="04dc0-328">Microsoft.PerceptionSimulation.ISimulationRecording</span><span class="sxs-lookup"><span data-stu-id="04dc0-328">Microsoft.PerceptionSimulation.ISimulationRecording</span></span>

<span data-ttu-id="04dc0-329">Charger de l’interface permettant d’interagir avec un enregistrement unique pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="04dc0-329">Interface for interacting with a single recording loaded for playback.</span></span>

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

<span data-ttu-id="04dc0-330">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span><span class="sxs-lookup"><span data-stu-id="04dc0-330">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span></span>

<span data-ttu-id="04dc0-331">Récupère la liste des types de données dans l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="04dc0-331">Retrieves the list of data types in the recording.</span></span>

<span data-ttu-id="04dc0-332">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span><span class="sxs-lookup"><span data-stu-id="04dc0-332">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span></span>

<span data-ttu-id="04dc0-333">Récupère l’état actuel de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="04dc0-333">Retrieves the current state of the recording.</span></span>

<span data-ttu-id="04dc0-334">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span><span class="sxs-lookup"><span data-stu-id="04dc0-334">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span></span>

<span data-ttu-id="04dc0-335">Démarrer la lecture.</span><span class="sxs-lookup"><span data-stu-id="04dc0-335">Start the playback.</span></span> <span data-ttu-id="04dc0-336">Si l’enregistrement est suspendue, la lecture reprend à partir de l’emplacement en pause ; Si arrêté, la lecture démarre au début.</span><span class="sxs-lookup"><span data-stu-id="04dc0-336">If the recording is paused, playback will resume from the paused location; if stopped, playback will start at the beginning.</span></span> <span data-ttu-id="04dc0-337">Si vous déjà des données, cet appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="04dc0-337">If already playing, this call is ignored.</span></span>

<span data-ttu-id="04dc0-338">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span><span class="sxs-lookup"><span data-stu-id="04dc0-338">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span></span>

<span data-ttu-id="04dc0-339">Suspend la lecture de son emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="04dc0-339">Pauses the playback at its current location.</span></span> <span data-ttu-id="04dc0-340">Si l’enregistrement est arrêté, l’appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="04dc0-340">If the recording is stopped, the call is ignored.</span></span>

<span data-ttu-id="04dc0-341">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-341">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span></span>

<span data-ttu-id="04dc0-342">Cherche de l’enregistrement à l’heure spécifiée (100 nanosecondes par intervalles d’à partir du début) et s’interrompt à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="04dc0-342">Seeks the recording to the specified time (in 100 nanoseconds intervals from the beginning) and pauses at that location.</span></span> <span data-ttu-id="04dc0-343">Si l’heure est après la fin de l’enregistrement, il est suspendu au niveau de la dernière image.</span><span class="sxs-lookup"><span data-stu-id="04dc0-343">If the time is beyond the end of the recording, it is paused at the last frame.</span></span>

<span data-ttu-id="04dc0-344">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-344">Parameters</span></span>
* <span data-ttu-id="04dc0-345">graduations - l’heure à laquelle effectuer une recherche</span><span class="sxs-lookup"><span data-stu-id="04dc0-345">ticks - The time to which to seek</span></span>

<span data-ttu-id="04dc0-346">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span><span class="sxs-lookup"><span data-stu-id="04dc0-346">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span></span>

<span data-ttu-id="04dc0-347">Arrête la lecture et réinitialise la position au début</span><span class="sxs-lookup"><span data-stu-id="04dc0-347">Stops the playback and resets the position to the beginning</span></span>

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a><span data-ttu-id="04dc0-348">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span><span class="sxs-lookup"><span data-stu-id="04dc0-348">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span></span>

<span data-ttu-id="04dc0-349">Interface pour la réception des modifications d’état pendant la lecture</span><span class="sxs-lookup"><span data-stu-id="04dc0-349">Interface for receiving state changes during playback</span></span>

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

<span data-ttu-id="04dc0-350">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-350">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span></span>

<span data-ttu-id="04dc0-351">Appelée lorsque l’état de la lecture d’un ISimulationRecording a changé</span><span class="sxs-lookup"><span data-stu-id="04dc0-351">Called when an ISimulationRecording's playback state has changed</span></span>

<span data-ttu-id="04dc0-352">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-352">Parameters</span></span>
* <span data-ttu-id="04dc0-353">newState - le nouvel état de l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="04dc0-353">newState - The new state of the recording</span></span>

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a><span data-ttu-id="04dc0-354">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="04dc0-354">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span></span>

<span data-ttu-id="04dc0-355">Objet racine pour la création d’objets de Simulation de Perception</span><span class="sxs-lookup"><span data-stu-id="04dc0-355">Root object for creating Perception Simulation objects</span></span>

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

<span data-ttu-id="04dc0-356">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-356">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span></span>

<span data-ttu-id="04dc0-357">Créer pour l’objet pour générer des paquets simulés et leur remise sur le récepteur fourni.</span><span class="sxs-lookup"><span data-stu-id="04dc0-357">Create on object for generating simulated packets and delivering them to the provided sink.</span></span>

<span data-ttu-id="04dc0-358">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-358">Parameters</span></span>
* <span data-ttu-id="04dc0-359">récepteur - le récepteur qui recevra toutes générées paquets</span><span class="sxs-lookup"><span data-stu-id="04dc0-359">sink - The sink that will receive all generated packets</span></span>

<span data-ttu-id="04dc0-360">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="04dc0-360">Return value</span></span>

<span data-ttu-id="04dc0-361">Le gestionnaire créé</span><span class="sxs-lookup"><span data-stu-id="04dc0-361">The created Manager</span></span>

<span data-ttu-id="04dc0-362">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-362">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span></span>

<span data-ttu-id="04dc0-363">Créer un récepteur qui stocke les paquets reçus tout dans un fichier sur le chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="04dc0-363">Create a sink which stores all received packets in a file at the specified path.</span></span>

<span data-ttu-id="04dc0-364">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-364">Parameters</span></span>
* <span data-ttu-id="04dc0-365">chemin d’accès - le chemin d’accès du fichier à créer</span><span class="sxs-lookup"><span data-stu-id="04dc0-365">path - The path of the file to create</span></span>

<span data-ttu-id="04dc0-366">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="04dc0-366">Return value</span></span>

<span data-ttu-id="04dc0-367">Le récepteur créé</span><span class="sxs-lookup"><span data-stu-id="04dc0-367">The created sink</span></span>

<span data-ttu-id="04dc0-368">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-368">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span></span>

<span data-ttu-id="04dc0-369">Charger un enregistrement à partir du fichier spécifié</span><span class="sxs-lookup"><span data-stu-id="04dc0-369">Load a recording from the specified file</span></span>

<span data-ttu-id="04dc0-370">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-370">Parameters</span></span>
* <span data-ttu-id="04dc0-371">chemin d’accès - le chemin d’accès du fichier à charger</span><span class="sxs-lookup"><span data-stu-id="04dc0-371">path - The path of the file to load</span></span>
* <span data-ttu-id="04dc0-372">Factory - une fabrique permettant de créer un ISimulationStreamSink lorsque requis par l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="04dc0-372">factory - A factory used by the recording for creating an ISimulationStreamSink when required</span></span>

<span data-ttu-id="04dc0-373">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="04dc0-373">Return value</span></span>

<span data-ttu-id="04dc0-374">L’enregistrement chargé</span><span class="sxs-lookup"><span data-stu-id="04dc0-374">The loaded recording</span></span>

<span data-ttu-id="04dc0-375">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording (System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory, Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-375">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory,Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span></span>

<span data-ttu-id="04dc0-376">Charger un enregistrement à partir du fichier spécifié</span><span class="sxs-lookup"><span data-stu-id="04dc0-376">Load a recording from the specified file</span></span>

<span data-ttu-id="04dc0-377">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-377">Parameters</span></span>
* <span data-ttu-id="04dc0-378">chemin d’accès - le chemin d’accès du fichier à charger</span><span class="sxs-lookup"><span data-stu-id="04dc0-378">path - The path of the file to load</span></span>
* <span data-ttu-id="04dc0-379">Factory - une fabrique permettant de créer un ISimulationStreamSink lorsque requis par l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="04dc0-379">factory - A factory used by the recording for creating an ISimulationStreamSink when required</span></span>
* <span data-ttu-id="04dc0-380">rappel - un rappel qui reçoit des mises à jour déclassement d’état de l’enregistrement</span><span class="sxs-lookup"><span data-stu-id="04dc0-380">callback - A callback which receives updates regrading the recording's status</span></span>

<span data-ttu-id="04dc0-381">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="04dc0-381">Return value</span></span>

<span data-ttu-id="04dc0-382">L’enregistrement chargé</span><span class="sxs-lookup"><span data-stu-id="04dc0-382">The loaded recording</span></span>

### <a name="microsoftperceptionsimulationstreamdatatypes"></a><span data-ttu-id="04dc0-383">Microsoft.PerceptionSimulation.StreamDataTypes</span><span class="sxs-lookup"><span data-stu-id="04dc0-383">Microsoft.PerceptionSimulation.StreamDataTypes</span></span>

<span data-ttu-id="04dc0-384">Décrit les différents types de données de flux</span><span class="sxs-lookup"><span data-stu-id="04dc0-384">Describes the different types of stream data</span></span>

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

<span data-ttu-id="04dc0-385">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span><span class="sxs-lookup"><span data-stu-id="04dc0-385">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span></span>

<span data-ttu-id="04dc0-386">Valeur de sentinelle permettant de n’indiquer aucun type de données de flux de données</span><span class="sxs-lookup"><span data-stu-id="04dc0-386">A sentinel value used to indicate no stream data types</span></span>

<span data-ttu-id="04dc0-387">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span><span class="sxs-lookup"><span data-stu-id="04dc0-387">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span></span>

<span data-ttu-id="04dc0-388">Stream des données relatives à la position et l’orientation de la tête</span><span class="sxs-lookup"><span data-stu-id="04dc0-388">Stream of data regarding the position and orientation of the head</span></span>

<span data-ttu-id="04dc0-389">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span><span class="sxs-lookup"><span data-stu-id="04dc0-389">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span></span>

<span data-ttu-id="04dc0-390">Stream de données sur la position et les mouvements de mains</span><span class="sxs-lookup"><span data-stu-id="04dc0-390">Stream of data regarding the position and gestures of hands</span></span>

<span data-ttu-id="04dc0-391">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span><span class="sxs-lookup"><span data-stu-id="04dc0-391">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span></span>

<span data-ttu-id="04dc0-392">Stream de données concernant le mappage spatial de l’environnement</span><span class="sxs-lookup"><span data-stu-id="04dc0-392">Stream of data regarding spatial mapping of the environment</span></span>

<span data-ttu-id="04dc0-393">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span><span class="sxs-lookup"><span data-stu-id="04dc0-393">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span></span>

<span data-ttu-id="04dc0-394">Stream de données concernant l’étalonnage de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="04dc0-394">Stream of data regarding calibration of the device.</span></span> <span data-ttu-id="04dc0-395">Paquets d’étalonnage sont uniquement acceptées par un système en Mode distant.</span><span class="sxs-lookup"><span data-stu-id="04dc0-395">Calibration packets are only accepted by a system in Remote Mode.</span></span>

<span data-ttu-id="04dc0-396">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span><span class="sxs-lookup"><span data-stu-id="04dc0-396">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span></span>

<span data-ttu-id="04dc0-397">Stream de données concernant l’environnement de l’appareil</span><span class="sxs-lookup"><span data-stu-id="04dc0-397">Stream of data regarding the environment of the device</span></span>

<span data-ttu-id="04dc0-398">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span><span class="sxs-lookup"><span data-stu-id="04dc0-398">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span></span>

<span data-ttu-id="04dc0-399">Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrées</span><span class="sxs-lookup"><span data-stu-id="04dc0-399">A sentinel value used to indicate all recorded data types</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a><span data-ttu-id="04dc0-400">Microsoft.PerceptionSimulation.ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="04dc0-400">Microsoft.PerceptionSimulation.ISimulationStreamSink</span></span>

<span data-ttu-id="04dc0-401">Objet qui reçoit des paquets de données à partir d’un flux de données de simulation</span><span class="sxs-lookup"><span data-stu-id="04dc0-401">An object that receives data packets from a simulation stream</span></span>

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

<span data-ttu-id="04dc0-402">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span><span class="sxs-lookup"><span data-stu-id="04dc0-402">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span></span>

<span data-ttu-id="04dc0-403">Reçoit un paquet unique, qui est en interne typés et avec contrôle de version</span><span class="sxs-lookup"><span data-stu-id="04dc0-403">Receives a single packet, which is internally typed and versioned</span></span>

<span data-ttu-id="04dc0-404">Paramètres</span><span class="sxs-lookup"><span data-stu-id="04dc0-404">Parameters</span></span>
* <span data-ttu-id="04dc0-405">Length - la longueur du paquet</span><span class="sxs-lookup"><span data-stu-id="04dc0-405">length - The length of the packet</span></span>
* <span data-ttu-id="04dc0-406">paquet - les données du paquet</span><span class="sxs-lookup"><span data-stu-id="04dc0-406">packet - The data of the packet</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a><span data-ttu-id="04dc0-407">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span><span class="sxs-lookup"><span data-stu-id="04dc0-407">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span></span>

<span data-ttu-id="04dc0-408">Un objet qui crée ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="04dc0-408">An object that creates ISimulationStreamSink</span></span>

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

<span data-ttu-id="04dc0-409">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span><span class="sxs-lookup"><span data-stu-id="04dc0-409">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span></span>

<span data-ttu-id="04dc0-410">Crée une instance unique de ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="04dc0-410">Creates a single instance of ISimulationStreamSink</span></span>

<span data-ttu-id="04dc0-411">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="04dc0-411">Return value</span></span>

<span data-ttu-id="04dc0-412">Le récepteur créé</span><span class="sxs-lookup"><span data-stu-id="04dc0-412">The created sink</span></span>
