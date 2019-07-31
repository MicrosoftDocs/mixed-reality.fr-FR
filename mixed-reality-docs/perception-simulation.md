---
title: Simulation de perception
description: Guide d’utilisation de la bibliothèque de simulation de perception pour automatiser une entrée simulée pour des applications immersifs
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
# <a name="perception-simulation"></a><span data-ttu-id="df69d-104">Simulation de perception</span><span class="sxs-lookup"><span data-stu-id="df69d-104">Perception simulation</span></span>

<span data-ttu-id="df69d-105">Voulez-vous créer un test automatisé pour votre application?</span><span class="sxs-lookup"><span data-stu-id="df69d-105">Do you want to build an automated test for your app?</span></span> <span data-ttu-id="df69d-106">Voulez-vous que vos tests vont au-delà des tests unitaires au niveau du composant et pour vraiment exercer votre application de bout en bout?</span><span class="sxs-lookup"><span data-stu-id="df69d-106">Do you want your tests to go beyond component-level unit testing and really exercise your app end-to-end?</span></span> <span data-ttu-id="df69d-107">La simulation de perception correspond à ce que vous recherchez.</span><span class="sxs-lookup"><span data-stu-id="df69d-107">Perception Simulation is what you're looking for.</span></span> <span data-ttu-id="df69d-108">La bibliothèque de simulation de perception envoie des données d’entrée humaines et mondiales à votre application afin que vous puissiez automatiser vos tests.</span><span class="sxs-lookup"><span data-stu-id="df69d-108">The Perception Simulation library sends human and world input data to your app so you can automate your tests.</span></span> <span data-ttu-id="df69d-109">Par exemple, vous pouvez simuler l’entrée d’un utilisateur cherchant à une position renouvelée et spécifique, puis d’effectuer un mouvement ou d’utiliser un contrôleur de mouvement.</span><span class="sxs-lookup"><span data-stu-id="df69d-109">For example, you can simulate the input of a human looking to a specific, repeatable position and then performing a gesture or using a motion controller.</span></span>

<span data-ttu-id="df69d-110">La simulation de perception peut envoyer une entrée simulée comme celle-ci à un HoloLens physique, à l’émulateur HoloLens (1ère génération), à l’émulateur HoloLens 2 ou à un PC avec portail de réalité mixte installé.</span><span class="sxs-lookup"><span data-stu-id="df69d-110">Perception Simulation can send simulated input like this to a physical HoloLens, the HoloLens emulator (1st gen), the HoloLens 2 Emulator, or a PC with Mixed Reality Portal installed.</span></span> <span data-ttu-id="df69d-111">La simulation de perception contourne les capteurs actifs sur un appareil de réalité mixte et envoie une entrée simulée aux applications qui s’exécutent sur l’appareil.</span><span class="sxs-lookup"><span data-stu-id="df69d-111">Perception Simulation bypasses the live sensors on a Mixed Reality device and sends simulated input to applications running on the device.</span></span> <span data-ttu-id="df69d-112">Les applications reçoivent ces événements d’entrée via les mêmes API qu’ils utilisent toujours et ne peuvent pas indiquer la différence entre l’exécution avec des capteurs réels et l’exécution avec la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="df69d-112">Applications receive these input events through the same APIs they always use and can't tell the difference between running with real sensors versus running with Perception Simulation.</span></span> <span data-ttu-id="df69d-113">La simulation de perception est la même technologie que celle utilisée par les émulateurs HoloLens pour envoyer une entrée simulée à la machine virtuelle HoloLens.</span><span class="sxs-lookup"><span data-stu-id="df69d-113">Perception Simulation is the same technology used by the HoloLens emulators to send simulated input to the HoloLens Virtual Machine.</span></span>

<span data-ttu-id="df69d-114">Pour commencer à utiliser la simulation dans votre code, commencez par créer un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="df69d-114">To begin using simulation in your code, start by creating an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="df69d-115">À partir de cet objet, vous pouvez émettre des commandes pour contrôler les propriétés d’un «humain» simulé, y compris la position de la tête, la position de la main et les gestes, et vous pouvez activer et manipuler les contrôleurs de mouvement.</span><span class="sxs-lookup"><span data-stu-id="df69d-115">From that object, you can issue commands to control properties of a simulated "human", including head position, hand position, and gestures, and you can enable and manipulate motion controllers.</span></span>

## <a name="setting-up-a-visual-studio-project-for-perception-simulation"></a><span data-ttu-id="df69d-116">Configuration d’un projet Visual Studio pour la simulation de perception</span><span class="sxs-lookup"><span data-stu-id="df69d-116">Setting Up a Visual Studio Project for Perception Simulation</span></span>
1. <span data-ttu-id="df69d-117">[Installez l’émulateur HoloLens](install-the-tools.md) sur votre PC de développement.</span><span class="sxs-lookup"><span data-stu-id="df69d-117">[Install the HoloLens emulator](install-the-tools.md) on your development PC.</span></span> <span data-ttu-id="df69d-118">L’émulateur comprend les bibliothèques que vous allez utiliser pour la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="df69d-118">The emulator includes the libraries you will use for Perception Simulation.</span></span>
2. <span data-ttu-id="df69d-119">Créez un projet de bureau C# Visual Studio (un projet de console fonctionne bien pour commencer).</span><span class="sxs-lookup"><span data-stu-id="df69d-119">Create a new Visual Studio C# desktop project (a Console Project works great to get started).</span></span>
3. <span data-ttu-id="df69d-120">Ajoutez les fichiers binaires suivants à votre projet en tant que références (Project-> Add-> Reference...). Vous pouvez les Rechercher dans% ProgramFiles (x86)% \ Microsoft XDE\\(version), par exemple **% ProgramFiles (x86)% \ Microsoft XDE\\10.0.18362.0** pour l’émulateur HoloLens 2.</span><span class="sxs-lookup"><span data-stu-id="df69d-120">Add the following binaries to your project as references (Project->Add->Reference...). You can find them in %ProgramFiles(x86)%\Microsoft XDE\\(version), such as **%ProgramFiles(x86)%\Microsoft XDE\\10.0.18362.0** for the HoloLens 2 Emulator.</span></span>  <span data-ttu-id="df69d-121">(Remarque: bien que les fichiers binaires fassent partie de l’émulateur HoloLens 2, ils fonctionnent également pour Windows Mixed Reality sur le bureau.) un.</span><span class="sxs-lookup"><span data-stu-id="df69d-121">(Note: although the binaries are part of the HoloLens 2 Emulator, they also work for Windows Mixed Reality on the desktop.) a.</span></span> <span data-ttu-id="df69d-122">PerceptionSimulationManager. Interop. dll-wrapper C# managé pour la simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="df69d-122">PerceptionSimulationManager.Interop.dll - Managed C# wrapper for Perception Simulation.</span></span>
    <span data-ttu-id="df69d-123">b.</span><span class="sxs-lookup"><span data-stu-id="df69d-123">b.</span></span> <span data-ttu-id="df69d-124">PerceptionSimulationRest. dll-Library pour la configuration d’un canal de communication de sockets Web vers le HoloLens ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="df69d-124">PerceptionSimulationRest.dll - Library for setting up a web-socket communication channel to the HoloLens or emulator.</span></span>
    <span data-ttu-id="df69d-125">c.</span><span class="sxs-lookup"><span data-stu-id="df69d-125">c.</span></span> <span data-ttu-id="df69d-126">SimulationStream. Interop. dll: types partagés pour la simulation.</span><span class="sxs-lookup"><span data-stu-id="df69d-126">SimulationStream.Interop.dll - Shared types for simulation.</span></span>
4. <span data-ttu-id="df69d-127">Ajoutez le fichier binaire d’implémentation PerceptionSimulationManager. dll à votre projet a.</span><span class="sxs-lookup"><span data-stu-id="df69d-127">Add the implementation binary PerceptionSimulationManager.dll to your project a.</span></span> <span data-ttu-id="df69d-128">Tout d’abord, ajoutez-le en tant que fichier binaire au projet (Project-> Ajouter > élément existant...). Enregistrez-le en tant que lien afin qu’il ne soit pas copié dans le dossier source de votre projet.</span><span class="sxs-lookup"><span data-stu-id="df69d-128">First add it as a binary to the project (Project->Add->Existing Item...). Save it as a link so that it doesn't copy it to your project source folder.</span></span> <span data-ttu-id="df69d-129">![Ajoutez PerceptionSimulationManager. dll au projet en tant que lien](images/saveaslink.png) b.</span><span class="sxs-lookup"><span data-stu-id="df69d-129">![Add PerceptionSimulationManager.dll to the project as a link](images/saveaslink.png) b.</span></span> <span data-ttu-id="df69d-130">Ensuite, assurez-vous qu’il est copié dans votre dossier de sortie lors de la génération.</span><span class="sxs-lookup"><span data-stu-id="df69d-130">Then make sure that it get's copied to your output folder on build.</span></span> <span data-ttu-id="df69d-131">Il s’agit de la feuille de propriétés pour le binaire.</span><span class="sxs-lookup"><span data-stu-id="df69d-131">This is in the property sheet for the binary .</span></span> <span data-ttu-id="df69d-132">![Marquer PerceptionSimulationManager. dll pour copier dans le répertoire de sortie](images/copyalways.png)</span><span class="sxs-lookup"><span data-stu-id="df69d-132">![Mark PerceptionSimulationManager.dll to copy to the output directory](images/copyalways.png)</span></span>
5. <span data-ttu-id="df69d-133">Définissez la plateforme de votre solution active sur x64.</span><span class="sxs-lookup"><span data-stu-id="df69d-133">Set your active solution platform to x64.</span></span>  <span data-ttu-id="df69d-134">(Utilisez la Configuration Manager pour créer une entrée de plateforme pour x64, si elle n’existe pas déjà.)</span><span class="sxs-lookup"><span data-stu-id="df69d-134">(Use the Configuration Manager to create a Platform entry for x64 if one does not already exist.)</span></span>

## <a name="creating-an-iperceptionsimulation-manager-object"></a><span data-ttu-id="df69d-135">Création d’un objet IPerceptionSimulation Manager</span><span class="sxs-lookup"><span data-stu-id="df69d-135">Creating an IPerceptionSimulation Manager Object</span></span>

<span data-ttu-id="df69d-136">Pour contrôler la simulation, vous allez émettre des mises à jour des objets récupérés à partir d’un objet IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="df69d-136">To control simulation, you'll issue updates to objects retrieved from an IPerceptionSimulationManager object.</span></span> <span data-ttu-id="df69d-137">La première étape consiste à obtenir cet objet et à le connecter à votre appareil ou émulateur cible.</span><span class="sxs-lookup"><span data-stu-id="df69d-137">The first step is to get that object and connect it to your target device or emulator.</span></span> <span data-ttu-id="df69d-138">Vous pouvez récupérer l’adresse IP de votre émulateur en cliquant sur le bouton du portail de l’appareil dans la [barre d’outils](using-the-hololens-emulator.md) .</span><span class="sxs-lookup"><span data-stu-id="df69d-138">You can get the IP address of your emulator by clicking on the Device Portal button in the [toolbar](using-the-hololens-emulator.md)</span></span>

<span data-ttu-id="df69d-139">![Icône](images/emulator-deviceportal.png) ouvrir le portail de l’appareil **ouvrir le portail**de l’appareil: ouvre le Portail d’appareil Windows pour le système d’exploitation HoloLens dans l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="df69d-139">![Open Device Portal icon](images/emulator-deviceportal.png) **Open Device Portal**: Open the Windows Device Portal for the HoloLens OS in the emulator.</span></span>  <span data-ttu-id="df69d-140">Pour Windows Mixed Reality, vous pouvez le récupérer dans l’application paramètres sous «mettre à jour & sécurité», puis «pour les développeurs» dans la section «se connecter à l’aide de» sous «activer le portail d’appareils».</span><span class="sxs-lookup"><span data-stu-id="df69d-140">For Windows Mixed Reality, this can be retrieved in the Settings app under "Update & Security", then "For developers" in the "Connect using:" section under "Enable Device Portal."</span></span>  <span data-ttu-id="df69d-141">Veillez à noter l’adresse IP et le port.</span><span class="sxs-lookup"><span data-stu-id="df69d-141">Be sure to note both the IP address and port.</span></span>

<span data-ttu-id="df69d-142">Tout d’abord, vous devez appeler RestSimulationStreamSink. Create pour obtenir un objet RestSimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="df69d-142">First, you'll call RestSimulationStreamSink.Create to get a RestSimulationStreamSink object.</span></span> <span data-ttu-id="df69d-143">Il s’agit de l’appareil ou de l’émulateur cible que vous allez contrôler sur une connexion http.</span><span class="sxs-lookup"><span data-stu-id="df69d-143">This is the target device or emulator that you will control over an http connection.</span></span> <span data-ttu-id="df69d-144">Vos commandes sont transmises à et gérées par le [portail de périphériques Windows](using-the-windows-device-portal.md) exécuté sur l’appareil ou l’émulateur.</span><span class="sxs-lookup"><span data-stu-id="df69d-144">Your commands will be passed to and handled by the [Windows Device Portal](using-the-windows-device-portal.md) running on the device or emulator.</span></span> <span data-ttu-id="df69d-145">Les quatre paramètres dont vous avez besoin pour créer un objet sont les suivants:</span><span class="sxs-lookup"><span data-stu-id="df69d-145">The four parameters you'll need to create an object are:</span></span>
* <span data-ttu-id="df69d-146">URI Uri: adresse IP de l’appareil cible (par exemple, "http://123.123.123.123 ou "http://123.123.123.123:50080")</span><span class="sxs-lookup"><span data-stu-id="df69d-146">Uri uri - IP address of the target device (e.g., "http://123.123.123.123" or "http://123.123.123.123:50080")</span></span>
* <span data-ttu-id="df69d-147">Informations d’identification System .net. NetworkCredential-nom d’utilisateur/mot de passe pour la connexion au [portail d’appareils Windows](using-the-windows-device-portal.md) sur l’appareil ou l’émulateur cible.</span><span class="sxs-lookup"><span data-stu-id="df69d-147">System.Net.NetworkCredential credentials - Username/password for connecting to the [Windows Device Portal](using-the-windows-device-portal.md) on the target device or emulator.</span></span> <span data-ttu-id="df69d-148">Si vous vous connectez à l’émulateur via son adresse locale (par exemple,*168..* . \*) sur le même PC, toutes les informations d’identification seront acceptées.</span><span class="sxs-lookup"><span data-stu-id="df69d-148">If you are connecting to the emulator via its local address (e.g., 168.*.*.\*) on the same PC, any credentials will be accepted.</span></span>
* <span data-ttu-id="df69d-149">bool normal-true pour la priorité normale, false pour basse priorité.</span><span class="sxs-lookup"><span data-stu-id="df69d-149">bool normal - True for normal priority, false for low priority.</span></span> <span data-ttu-id="df69d-150">Vous souhaitez généralement définir cette propriété sur *true* pour les scénarios de test, ce qui permet à votre test de prendre le contrôle.</span><span class="sxs-lookup"><span data-stu-id="df69d-150">You generally want to set this to *true* for test scenarios, which allows your test to take control.</span></span>  <span data-ttu-id="df69d-151">La simulation de l’émulateur et de la réalité mixte Windows utilise des connexions de faible priorité.</span><span class="sxs-lookup"><span data-stu-id="df69d-151">The emulator and Windows Mixed Reality simulation use low priority connections.</span></span>  <span data-ttu-id="df69d-152">Si votre test utilise également une connexion de faible priorité, la connexion établie le plus récemment sera Control.</span><span class="sxs-lookup"><span data-stu-id="df69d-152">If your test also uses a low priority connection, the most recently established connection will be in control.</span></span>
* <span data-ttu-id="df69d-153">Jeton-jeton System. Threading. CancellationToken pour annuler l’opération asynchrone.</span><span class="sxs-lookup"><span data-stu-id="df69d-153">System.Threading.CancellationToken token - Token to cancel the async operation.</span></span>

<span data-ttu-id="df69d-154">Ensuite, vous allez créer le IPerceptionSimulationManager.</span><span class="sxs-lookup"><span data-stu-id="df69d-154">Second you will create the IPerceptionSimulationManager.</span></span> <span data-ttu-id="df69d-155">Il s’agit de l’objet que vous utilisez pour contrôler la simulation.</span><span class="sxs-lookup"><span data-stu-id="df69d-155">This is the object you use to control simulation.</span></span> <span data-ttu-id="df69d-156">Notez que cela doit également être fait dans une méthode Async.</span><span class="sxs-lookup"><span data-stu-id="df69d-156">Note that this must also be done in an async method.</span></span>

## <a name="control-the-simulated-human"></a><span data-ttu-id="df69d-157">Contrôler l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-157">Control the simulated Human</span></span>

<span data-ttu-id="df69d-158">Un IPerceptionSimulationManager a une propriété humaine qui retourne un objet ISimulatedHuman.</span><span class="sxs-lookup"><span data-stu-id="df69d-158">An IPerceptionSimulationManager has a Human property that returns an ISimulatedHuman object.</span></span> <span data-ttu-id="df69d-159">Pour contrôler l’homme simulé, effectuez des opérations sur cet objet.</span><span class="sxs-lookup"><span data-stu-id="df69d-159">To control the simulated human, perform operations on this object.</span></span> <span data-ttu-id="df69d-160">Exemple :</span><span class="sxs-lookup"><span data-stu-id="df69d-160">For example:</span></span>

```
manager.Human.Move(new Vector3(0.1f, 0.0f, 0.0f))
```

## <a name="basic-sample-c-console-application"></a><span data-ttu-id="df69d-161">Exemple C# d’application console de base</span><span class="sxs-lookup"><span data-stu-id="df69d-161">Basic Sample C# console application</span></span>

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

## <a name="extended-sample-c-console-application"></a><span data-ttu-id="df69d-162">Exemple C# d’application console étendue</span><span class="sxs-lookup"><span data-stu-id="df69d-162">Extended Sample C# console application</span></span>

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

## <a name="note-on-6-dof-controllers"></a><span data-ttu-id="df69d-163">Remarque sur les contrôleurs 6-DDL</span><span class="sxs-lookup"><span data-stu-id="df69d-163">Note on 6-DOF controllers</span></span>

<span data-ttu-id="df69d-164">Avant d’appeler des propriétés sur des méthodes sur un contrôleur 6-DDL simulé, vous devez activer le contrôleur.</span><span class="sxs-lookup"><span data-stu-id="df69d-164">Before calling any properties on methods on a simulated 6-DOF controller, you must activate the controller.</span></span>  <span data-ttu-id="df69d-165">Si ce n’est pas le cas, une exception est générée.</span><span class="sxs-lookup"><span data-stu-id="df69d-165">Not doing so will result in an exception.</span></span>  <span data-ttu-id="df69d-166">À compter de la mise à jour de Windows 10 2019 mai, les contrôleurs 6-DDL simulés peuvent être installés et activés en définissant la propriété Status sur l’objet ISimulatedSixDofController sur SimulatedSixDofControllerStatus. active.</span><span class="sxs-lookup"><span data-stu-id="df69d-166">Starting with the Windows 10 May 2019 Update, simulated 6-DOF controllers can be installed and activated by setting the Status property on the ISimulatedSixDofController object to SimulatedSixDofControllerStatus.Active.</span></span>
<span data-ttu-id="df69d-167">Dans la mise à jour 2018 de Windows 10 octobre et les versions antérieures, vous devez d’abord installer séparément un contrôleur 6-DDL simulé en appelant l’outil PerceptionSimulationDevice situé dans le dossier \Windows\System32.</span><span class="sxs-lookup"><span data-stu-id="df69d-167">In the Windows 10 October 2018 Update and earlier, you must separately install a simulated 6-DOF controller first by calling the PerceptionSimulationDevice tool located in the \Windows\System32 folder.</span></span>  <span data-ttu-id="df69d-168">L’utilisation de cet outil est la suivante:</span><span class="sxs-lookup"><span data-stu-id="df69d-168">The usage of this tool is as follows:</span></span>


```
    PerceptionSimulationDevice.exe <action> 6dof <instance>
```

<span data-ttu-id="df69d-169">Exemple :</span><span class="sxs-lookup"><span data-stu-id="df69d-169">For example</span></span>

```
    PerceptionSimulationDevice.exe i 6dof 1
```

<span data-ttu-id="df69d-170">Les actions prises en charge sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="df69d-170">Supported actions are:</span></span>
* <span data-ttu-id="df69d-171">i = installation</span><span class="sxs-lookup"><span data-stu-id="df69d-171">i = install</span></span>
* <span data-ttu-id="df69d-172">q = requête</span><span class="sxs-lookup"><span data-stu-id="df69d-172">q = query</span></span>
* <span data-ttu-id="df69d-173">r = supprimer</span><span class="sxs-lookup"><span data-stu-id="df69d-173">r = remove</span></span>

<span data-ttu-id="df69d-174">Les instances prises en charge sont les suivantes:</span><span class="sxs-lookup"><span data-stu-id="df69d-174">Supported instances are:</span></span>
* <span data-ttu-id="df69d-175">1 = le contrôleur 6-DDL de gauche</span><span class="sxs-lookup"><span data-stu-id="df69d-175">1 = the left 6-DOF controller</span></span>
* <span data-ttu-id="df69d-176">2 = le contrôleur 6-DDL correct</span><span class="sxs-lookup"><span data-stu-id="df69d-176">2 = the right 6-DOF controller</span></span>

<span data-ttu-id="df69d-177">Le code de sortie du processus indique la réussite (valeur de retour zéro) ou l’échec (valeur de retour différente de zéro).</span><span class="sxs-lookup"><span data-stu-id="df69d-177">The exit code of the process will indicate success (a zero return value) or failure (a non-zero return value).</span></span>  <span data-ttu-id="df69d-178">Lorsque vous utilisez l’action q pour demander si un contrôleur est installé ou non, la valeur de retour est zéro (0) si le contrôleur n’est pas déjà installé ou un (1) si le contrôleur est installé.</span><span class="sxs-lookup"><span data-stu-id="df69d-178">When using the 'q' action to query whether or not a controller is installed, the return value will be zero (0) if the controller is not already installed or one (1) if the controller is installed.</span></span>

<span data-ttu-id="df69d-179">Lorsque vous supprimez un contrôleur sur la mise à jour 2018 de Windows 10 octobre ou une version antérieure, définissez son état sur OFF via l’API en premier, puis appelez l’outil PerceptionSimulationDevice.</span><span class="sxs-lookup"><span data-stu-id="df69d-179">When removing a controller on the Windows 10 October 2018 Update or earlier, set its status to Off via the API first, then call the PerceptionSimulationDevice tool.</span></span>

<span data-ttu-id="df69d-180">Notez que cet outil doit être exécuté en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="df69d-180">Note that this tool must be run as Administrator.</span></span>




## <a name="api-reference"></a><span data-ttu-id="df69d-181">Référence de l’API</span><span class="sxs-lookup"><span data-stu-id="df69d-181">API Reference</span></span>

### <a name="microsoftperceptionsimulationsimulateddevicetype"></a><span data-ttu-id="df69d-182">Microsoft. PerceptionSimulation. SimulatedDeviceType</span><span class="sxs-lookup"><span data-stu-id="df69d-182">Microsoft.PerceptionSimulation.SimulatedDeviceType</span></span>

<span data-ttu-id="df69d-183">Décrit un type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-183">Describes a simulated device type</span></span>

```
public enum SimulatedDeviceType
{
    Reference = 0
}
```

<span data-ttu-id="df69d-184">**Microsoft. PerceptionSimulation. SimulatedDeviceType. Reference**</span><span class="sxs-lookup"><span data-stu-id="df69d-184">**Microsoft.PerceptionSimulation.SimulatedDeviceType.Reference**</span></span>

<span data-ttu-id="df69d-185">Un appareil de référence fictif, la valeur par défaut pour PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="df69d-185">A fictitious reference device, the default for PerceptionSimulationManager</span></span>

### <a name="microsoftperceptionsimulationheadtrackermode"></a><span data-ttu-id="df69d-186">Microsoft. PerceptionSimulation. HeadTrackerMode</span><span class="sxs-lookup"><span data-stu-id="df69d-186">Microsoft.PerceptionSimulation.HeadTrackerMode</span></span>

<span data-ttu-id="df69d-187">Décrit un mode de suivi d’en-tête</span><span class="sxs-lookup"><span data-stu-id="df69d-187">Describes a head tracker mode</span></span>

```
public enum HeadTrackerMode
{
    Default = 0,
    Orientation = 1,
    Position = 2
}
```

<span data-ttu-id="df69d-188">**Microsoft. PerceptionSimulation. HeadTrackerMode. default**</span><span class="sxs-lookup"><span data-stu-id="df69d-188">**Microsoft.PerceptionSimulation.HeadTrackerMode.Default**</span></span>

<span data-ttu-id="df69d-189">Suivi des en-têtes par défaut.</span><span class="sxs-lookup"><span data-stu-id="df69d-189">Default Head Tracking.</span></span> <span data-ttu-id="df69d-190">Cela signifie que le système peut sélectionner le mode de suivi optimal en fonction des conditions d’exécution.</span><span class="sxs-lookup"><span data-stu-id="df69d-190">This means the system may select the best head tracking mode based upon runtime conditions.</span></span>

<span data-ttu-id="df69d-191">**Microsoft. PerceptionSimulation. HeadTrackerMode. orientation**</span><span class="sxs-lookup"><span data-stu-id="df69d-191">**Microsoft.PerceptionSimulation.HeadTrackerMode.Orientation**</span></span>

<span data-ttu-id="df69d-192">Suivi d’en-tête d’orientation uniquement.</span><span class="sxs-lookup"><span data-stu-id="df69d-192">Orientation Only Head Tracking.</span></span> <span data-ttu-id="df69d-193">Cela signifie que la position suivie peut ne pas être fiable, et certaines fonctionnalités qui dépendent de la position de la tête peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="df69d-193">This means that the tracked position may not be reliable, and some functionality dependent on head position may not be available.</span></span>

<span data-ttu-id="df69d-194">**Microsoft. PerceptionSimulation. HeadTrackerMode. position**</span><span class="sxs-lookup"><span data-stu-id="df69d-194">**Microsoft.PerceptionSimulation.HeadTrackerMode.Position**</span></span>

<span data-ttu-id="df69d-195">Suivi de l’en-tête positionnel.</span><span class="sxs-lookup"><span data-stu-id="df69d-195">Positional Head Tracking.</span></span> <span data-ttu-id="df69d-196">Cela signifie que la position et l’orientation de la tête de suivi sont fiables</span><span class="sxs-lookup"><span data-stu-id="df69d-196">This means that the tracked head position and orientation are both reliable</span></span>

### <a name="microsoftperceptionsimulationsimulatedgesture"></a><span data-ttu-id="df69d-197">Microsoft. PerceptionSimulation. SimulatedGesture</span><span class="sxs-lookup"><span data-stu-id="df69d-197">Microsoft.PerceptionSimulation.SimulatedGesture</span></span>

<span data-ttu-id="df69d-198">Décrit un mouvement simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-198">Describes a simulated gesture</span></span>

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

<span data-ttu-id="df69d-199">**Microsoft. PerceptionSimulation. SimulatedGesture. None**</span><span class="sxs-lookup"><span data-stu-id="df69d-199">**Microsoft.PerceptionSimulation.SimulatedGesture.None**</span></span>

<span data-ttu-id="df69d-200">Valeur de sentinelle utilisée pour indiquer l’absence de gestes.</span><span class="sxs-lookup"><span data-stu-id="df69d-200">A sentinel value used to indicate no gestures.</span></span>

<span data-ttu-id="df69d-201">**Microsoft. PerceptionSimulation. SimulatedGesture. FingerPressed**</span><span class="sxs-lookup"><span data-stu-id="df69d-201">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerPressed**</span></span>

<span data-ttu-id="df69d-202">Mouvement appuyé sur le doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-202">A finger pressed gesture.</span></span>

<span data-ttu-id="df69d-203">**Microsoft. PerceptionSimulation. SimulatedGesture. FingerReleased**</span><span class="sxs-lookup"><span data-stu-id="df69d-203">**Microsoft.PerceptionSimulation.SimulatedGesture.FingerReleased**</span></span>

<span data-ttu-id="df69d-204">Mouvement de libération d’un doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-204">A finger released gesture.</span></span>

<span data-ttu-id="df69d-205">**Microsoft. PerceptionSimulation. SimulatedGesture. orig**</span><span class="sxs-lookup"><span data-stu-id="df69d-205">**Microsoft.PerceptionSimulation.SimulatedGesture.Home**</span></span>

<span data-ttu-id="df69d-206">Mouvement de démarrage/système.</span><span class="sxs-lookup"><span data-stu-id="df69d-206">The home/system gesture.</span></span>

<span data-ttu-id="df69d-207">**Microsoft. PerceptionSimulation. SimulatedGesture. Max**</span><span class="sxs-lookup"><span data-stu-id="df69d-207">**Microsoft.PerceptionSimulation.SimulatedGesture.Max**</span></span>

<span data-ttu-id="df69d-208">Mouvement maximal valide.</span><span class="sxs-lookup"><span data-stu-id="df69d-208">The maximum valid gesture.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerstatus"></a><span data-ttu-id="df69d-209">Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus</span><span class="sxs-lookup"><span data-stu-id="df69d-209">Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus</span></span>

<span data-ttu-id="df69d-210">États possibles d’un contrôleur 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-210">The possible states of a simulated 6-DOF controller.</span></span>

```
public enum SimulatedSixDofControllerStatus
{
    Off = 0,
    Active = 1,
    TrackingLost = 2,
}
```

<span data-ttu-id="df69d-211">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. OFF**</span><span class="sxs-lookup"><span data-stu-id="df69d-211">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Off**</span></span>

<span data-ttu-id="df69d-212">Le contrôleur 6-DDL est désactivé.</span><span class="sxs-lookup"><span data-stu-id="df69d-212">The 6-DOF controller is turned off.</span></span>

<span data-ttu-id="df69d-213">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. active**</span><span class="sxs-lookup"><span data-stu-id="df69d-213">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.Active**</span></span>

<span data-ttu-id="df69d-214">Le contrôleur 6-DDL est activé et suivi.</span><span class="sxs-lookup"><span data-stu-id="df69d-214">The 6-DOF controller is turned on and tracked.</span></span>

<span data-ttu-id="df69d-215">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerStatus. TrackingLost**</span><span class="sxs-lookup"><span data-stu-id="df69d-215">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerStatus.TrackingLost**</span></span>

<span data-ttu-id="df69d-216">Le contrôleur 6-DDL est activé, mais ne peut pas être suivi.</span><span class="sxs-lookup"><span data-stu-id="df69d-216">The 6-DOF controller is turned on but cannot be tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedsixdofcontrollerbutton"></a><span data-ttu-id="df69d-217">Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton</span><span class="sxs-lookup"><span data-stu-id="df69d-217">Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton</span></span>

<span data-ttu-id="df69d-218">Les boutons pris en charge sur un contrôleur 6-DDL simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-218">The supported buttons on a simulated 6-DOF controller.</span></span>

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

<span data-ttu-id="df69d-219">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. None**</span><span class="sxs-lookup"><span data-stu-id="df69d-219">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.None**</span></span>

<span data-ttu-id="df69d-220">Valeur de sentinelle utilisée pour indiquer qu’aucun bouton n’est présent.</span><span class="sxs-lookup"><span data-stu-id="df69d-220">A sentinel value used to indicate no buttons.</span></span>

<span data-ttu-id="df69d-221">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. orig**</span><span class="sxs-lookup"><span data-stu-id="df69d-221">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Home**</span></span>

<span data-ttu-id="df69d-222">Le bouton d’hébergement est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-222">The Home button is pressed.</span></span>

<span data-ttu-id="df69d-223">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. menu**</span><span class="sxs-lookup"><span data-stu-id="df69d-223">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Menu**</span></span>

<span data-ttu-id="df69d-224">Le bouton de menu est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-224">The Menu button is pressed.</span></span>

<span data-ttu-id="df69d-225">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. poignée**</span><span class="sxs-lookup"><span data-stu-id="df69d-225">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Grip**</span></span>

<span data-ttu-id="df69d-226">Le bouton de la poignée est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-226">The Grip button is pressed.</span></span>

<span data-ttu-id="df69d-227">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadPress**</span><span class="sxs-lookup"><span data-stu-id="df69d-227">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadPress**</span></span>

<span data-ttu-id="df69d-228">Le pavé tactile est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-228">The TouchPad is pressed.</span></span>

<span data-ttu-id="df69d-229">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Select**</span><span class="sxs-lookup"><span data-stu-id="df69d-229">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Select**</span></span>

<span data-ttu-id="df69d-230">Le bouton Sélectionner est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-230">The Select button is pressed.</span></span>

<span data-ttu-id="df69d-231">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. TouchpadTouch**</span><span class="sxs-lookup"><span data-stu-id="df69d-231">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.TouchpadTouch**</span></span>

<span data-ttu-id="df69d-232">Le pavé tactile est touché.</span><span class="sxs-lookup"><span data-stu-id="df69d-232">The TouchPad is touched.</span></span>

<span data-ttu-id="df69d-233">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Stick**</span><span class="sxs-lookup"><span data-stu-id="df69d-233">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Thumbstick**</span></span>

<span data-ttu-id="df69d-234">Le stick analogique est enfoncé.</span><span class="sxs-lookup"><span data-stu-id="df69d-234">The Thumbstick is pressed.</span></span>

<span data-ttu-id="df69d-235">**Microsoft. PerceptionSimulation. SimulatedSixDofControllerButton. Max**</span><span class="sxs-lookup"><span data-stu-id="df69d-235">**Microsoft.PerceptionSimulation.SimulatedSixDofControllerButton.Max**</span></span>

<span data-ttu-id="df69d-236">Le bouton nombre maximal valide.</span><span class="sxs-lookup"><span data-stu-id="df69d-236">The maximum valid button.</span></span>


### <a name="microsoftperceptionsimulationsimulatedeyescalibrationstate"></a><span data-ttu-id="df69d-237">Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState</span><span class="sxs-lookup"><span data-stu-id="df69d-237">Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState</span></span>

<span data-ttu-id="df69d-238">État d’étalonnage des yeux simulés</span><span class="sxs-lookup"><span data-stu-id="df69d-238">The calibration state of the simulated eyes</span></span>

```
public enum SimulatedGesture
{
    Unavailable = 0,
    Ready = 1,
    Configuring = 2,
    UserCalibrationNeeded = 3
}
```

<span data-ttu-id="df69d-239">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. non disponible**</span><span class="sxs-lookup"><span data-stu-id="df69d-239">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Unavailable**</span></span>

<span data-ttu-id="df69d-240">L’étalonnage des yeux n’est pas disponible.</span><span class="sxs-lookup"><span data-stu-id="df69d-240">The eyes calibration is unavailable.</span></span>

<span data-ttu-id="df69d-241">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Ready**</span><span class="sxs-lookup"><span data-stu-id="df69d-241">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Ready**</span></span>

<span data-ttu-id="df69d-242">Les yeux ont été étalonnés.</span><span class="sxs-lookup"><span data-stu-id="df69d-242">The eyes have been calibrated.</span></span>  <span data-ttu-id="df69d-243">Valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="df69d-243">This is the default value.</span></span>

<span data-ttu-id="df69d-244">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. Configuration**</span><span class="sxs-lookup"><span data-stu-id="df69d-244">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.Configuring**</span></span>

<span data-ttu-id="df69d-245">Les yeux sont calibrés.</span><span class="sxs-lookup"><span data-stu-id="df69d-245">The eyes are being calibrated.</span></span>

<span data-ttu-id="df69d-246">**Microsoft. PerceptionSimulation. SimulatedEyesCalibrationState. UserCalibrationNeeded**</span><span class="sxs-lookup"><span data-stu-id="df69d-246">**Microsoft.PerceptionSimulation.SimulatedEyesCalibrationState.UserCalibrationNeeded**</span></span>

<span data-ttu-id="df69d-247">Les yeux doivent être étalonnés.</span><span class="sxs-lookup"><span data-stu-id="df69d-247">The eyes need to be calibrated.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointtrackingaccuracy"></a><span data-ttu-id="df69d-248">Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy</span><span class="sxs-lookup"><span data-stu-id="df69d-248">Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy</span></span>

<span data-ttu-id="df69d-249">Précision de suivi d’une jointure de la main.</span><span class="sxs-lookup"><span data-stu-id="df69d-249">The tracking accuracy of a joint of the hand.</span></span>

```
public enum SimulatedHandJointTrackingAccuracy
{
    Unavailable = 0,
    Approximate = 1,
    Visible = 2
}
```

<span data-ttu-id="df69d-250">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. non disponible**</span><span class="sxs-lookup"><span data-stu-id="df69d-250">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Unavailable**</span></span>

<span data-ttu-id="df69d-251">La jointure n’est pas suivie.</span><span class="sxs-lookup"><span data-stu-id="df69d-251">The joint is not tracked.</span></span>

<span data-ttu-id="df69d-252">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. approximatif**</span><span class="sxs-lookup"><span data-stu-id="df69d-252">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Approximate**</span></span>

<span data-ttu-id="df69d-253">La position conjointe est déduite.</span><span class="sxs-lookup"><span data-stu-id="df69d-253">The joint position is inferred.</span></span>

<span data-ttu-id="df69d-254">**Microsoft. PerceptionSimulation. SimulatedHandJointTrackingAccuracy. visible**</span><span class="sxs-lookup"><span data-stu-id="df69d-254">**Microsoft.PerceptionSimulation.SimulatedHandJointTrackingAccuracy.Visible**</span></span>

<span data-ttu-id="df69d-255">L’articulation est entièrement suivie.</span><span class="sxs-lookup"><span data-stu-id="df69d-255">The joint is fully tracked.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandpose"></a><span data-ttu-id="df69d-256">Microsoft. PerceptionSimulation. SimulatedHandPose</span><span class="sxs-lookup"><span data-stu-id="df69d-256">Microsoft.PerceptionSimulation.SimulatedHandPose</span></span>

<span data-ttu-id="df69d-257">Précision de suivi d’une jointure de la main.</span><span class="sxs-lookup"><span data-stu-id="df69d-257">The tracking accuracy of a joint of the hand.</span></span>

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

<span data-ttu-id="df69d-258">**Microsoft. PerceptionSimulation. SimulatedHandPose. Closed**</span><span class="sxs-lookup"><span data-stu-id="df69d-258">**Microsoft.PerceptionSimulation.SimulatedHandPose.Closed**</span></span>

<span data-ttu-id="df69d-259">Les jointures Finger de la main sont configurées pour refléter une pose fermée.</span><span class="sxs-lookup"><span data-stu-id="df69d-259">The hand's finger joints are configured to reflect a closed pose.</span></span>

<span data-ttu-id="df69d-260">**Microsoft. PerceptionSimulation. SimulatedHandPose. Open**</span><span class="sxs-lookup"><span data-stu-id="df69d-260">**Microsoft.PerceptionSimulation.SimulatedHandPose.Open**</span></span>

<span data-ttu-id="df69d-261">Les jointures Finger de la main sont configurées pour refléter une pose ouverte.</span><span class="sxs-lookup"><span data-stu-id="df69d-261">The hand's finger joints are configured to reflect an open pose.</span></span>

<span data-ttu-id="df69d-262">**Microsoft. PerceptionSimulation. SimulatedHandPose. point**</span><span class="sxs-lookup"><span data-stu-id="df69d-262">**Microsoft.PerceptionSimulation.SimulatedHandPose.Point**</span></span>

<span data-ttu-id="df69d-263">Les jointures Finger de la main sont configurées pour refléter une pose de pointage.</span><span class="sxs-lookup"><span data-stu-id="df69d-263">The hand's finger joints are configured to reflect a pointing pose.</span></span>

<span data-ttu-id="df69d-264">**Microsoft. PerceptionSimulation. SimulatedHandPose. pincement**</span><span class="sxs-lookup"><span data-stu-id="df69d-264">**Microsoft.PerceptionSimulation.SimulatedHandPose.Pinch**</span></span>

<span data-ttu-id="df69d-265">Les jointures Finger de la main sont configurées pour refléter une pose de pincement.</span><span class="sxs-lookup"><span data-stu-id="df69d-265">The hand's finger joints are configured to reflect a pinching pose.</span></span>

<span data-ttu-id="df69d-266">**Microsoft. PerceptionSimulation. SimulatedHandPose. Max**</span><span class="sxs-lookup"><span data-stu-id="df69d-266">**Microsoft.PerceptionSimulation.SimulatedHandPose.Max**</span></span>

<span data-ttu-id="df69d-267">Valeur maximale valide pour SimulatedHandPose.</span><span class="sxs-lookup"><span data-stu-id="df69d-267">The maximum valid value for SimulatedHandPose.</span></span>


### <a name="microsoftperceptionsimulationplaybackstate"></a><span data-ttu-id="df69d-268">Microsoft. PerceptionSimulation. PlaybackState</span><span class="sxs-lookup"><span data-stu-id="df69d-268">Microsoft.PerceptionSimulation.PlaybackState</span></span>

<span data-ttu-id="df69d-269">Décrit l’état d’une lecture.</span><span class="sxs-lookup"><span data-stu-id="df69d-269">Describes the state of a playback.</span></span>

```
public enum PlaybackState
{
    Stopped = 0,
    Playing = 1,
    Paused = 2,
    End = 3,
}
```

<span data-ttu-id="df69d-270">**Microsoft. PerceptionSimulation. PlaybackState. Stopped**</span><span class="sxs-lookup"><span data-stu-id="df69d-270">**Microsoft.PerceptionSimulation.PlaybackState.Stopped**</span></span>

<span data-ttu-id="df69d-271">L’enregistrement est actuellement arrêté et prêt pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="df69d-271">The recording is currently stopped and ready for playback.</span></span>

<span data-ttu-id="df69d-272">**Microsoft. PerceptionSimulation. PlaybackState. Playing**</span><span class="sxs-lookup"><span data-stu-id="df69d-272">**Microsoft.PerceptionSimulation.PlaybackState.Playing**</span></span>

<span data-ttu-id="df69d-273">L’enregistrement est en cours de diffusion.</span><span class="sxs-lookup"><span data-stu-id="df69d-273">The recording is currently playing.</span></span>

<span data-ttu-id="df69d-274">**Microsoft. PerceptionSimulation. PlaybackState. Paused**</span><span class="sxs-lookup"><span data-stu-id="df69d-274">**Microsoft.PerceptionSimulation.PlaybackState.Paused**</span></span>

<span data-ttu-id="df69d-275">L’enregistrement est actuellement suspendu.</span><span class="sxs-lookup"><span data-stu-id="df69d-275">The recording is currently paused.</span></span>

<span data-ttu-id="df69d-276">**Microsoft. PerceptionSimulation. PlaybackState. end**</span><span class="sxs-lookup"><span data-stu-id="df69d-276">**Microsoft.PerceptionSimulation.PlaybackState.End**</span></span>

<span data-ttu-id="df69d-277">L’enregistrement a atteint la fin.</span><span class="sxs-lookup"><span data-stu-id="df69d-277">The recording has reached the end.</span></span>

### <a name="microsoftperceptionsimulationvector3"></a><span data-ttu-id="df69d-278">Microsoft. PerceptionSimulation. Vector3</span><span class="sxs-lookup"><span data-stu-id="df69d-278">Microsoft.PerceptionSimulation.Vector3</span></span>

<span data-ttu-id="df69d-279">Décrit un vecteur de 3 composants, qui peut décrire un point ou un vecteur dans l’espace 3D.</span><span class="sxs-lookup"><span data-stu-id="df69d-279">Describes a 3 components vector, which might describe a point or a vector in 3D space.</span></span>

```
public struct Vector3
{
    public float X;
    public float Y;
    public float Z;
    public Vector3(float x, float y, float z);
}
```

<span data-ttu-id="df69d-280">**Microsoft. PerceptionSimulation. Vector3. X**</span><span class="sxs-lookup"><span data-stu-id="df69d-280">**Microsoft.PerceptionSimulation.Vector3.X**</span></span>

<span data-ttu-id="df69d-281">Composant X du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-281">The X component of the vector.</span></span>

<span data-ttu-id="df69d-282">**Microsoft. PerceptionSimulation. Vector3. Y**</span><span class="sxs-lookup"><span data-stu-id="df69d-282">**Microsoft.PerceptionSimulation.Vector3.Y**</span></span>

<span data-ttu-id="df69d-283">Composant Y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-283">The Y component of the vector.</span></span>

<span data-ttu-id="df69d-284">**Microsoft. PerceptionSimulation. Vector3. Z**</span><span class="sxs-lookup"><span data-stu-id="df69d-284">**Microsoft.PerceptionSimulation.Vector3.Z**</span></span>

<span data-ttu-id="df69d-285">Composant Z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-285">The Z component of the vector.</span></span>

<span data-ttu-id="df69d-286">**Microsoft. PerceptionSimulation. Vector3. #ctor (System. Single, System. Single, System. Single)**</span><span class="sxs-lookup"><span data-stu-id="df69d-286">**Microsoft.PerceptionSimulation.Vector3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="df69d-287">Construisez un nouveau Vector3.</span><span class="sxs-lookup"><span data-stu-id="df69d-287">Construct a new Vector3.</span></span>

<span data-ttu-id="df69d-288">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-288">Parameters</span></span>
* <span data-ttu-id="df69d-289">x-composant x du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-289">x - The x component of the vector.</span></span>
* <span data-ttu-id="df69d-290">y: composant y du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-290">y - The y component of the vector.</span></span>
* <span data-ttu-id="df69d-291">z-composant z du vecteur.</span><span class="sxs-lookup"><span data-stu-id="df69d-291">z - The z component of the vector.</span></span>

### <a name="microsoftperceptionsimulationrotation3"></a><span data-ttu-id="df69d-292">Microsoft. PerceptionSimulation. Rotation3</span><span class="sxs-lookup"><span data-stu-id="df69d-292">Microsoft.PerceptionSimulation.Rotation3</span></span>

<span data-ttu-id="df69d-293">Décrit une rotation de 3 composants.</span><span class="sxs-lookup"><span data-stu-id="df69d-293">Describes a 3 components rotation.</span></span>

```
public struct Rotation3
{
    public float Pitch;
    public float Yaw;
    public float Roll;
    public Rotation3(float pitch, float yaw, float roll);
}
```

<span data-ttu-id="df69d-294">**Microsoft. PerceptionSimulation. Rotation3. brai**</span><span class="sxs-lookup"><span data-stu-id="df69d-294">**Microsoft.PerceptionSimulation.Rotation3.Pitch**</span></span>

<span data-ttu-id="df69d-295">Composant de pas de la rotation, en hauteur autour de l’axe X.</span><span class="sxs-lookup"><span data-stu-id="df69d-295">The Pitch component of the Rotation, down around the X axis.</span></span>

<span data-ttu-id="df69d-296">**Microsoft. PerceptionSimulation. Rotation3. lacet**</span><span class="sxs-lookup"><span data-stu-id="df69d-296">**Microsoft.PerceptionSimulation.Rotation3.Yaw**</span></span>

<span data-ttu-id="df69d-297">Composant de lacet de la rotation, à droite autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="df69d-297">The Yaw component of the Rotation, right around the Y axis.</span></span>

<span data-ttu-id="df69d-298">**Microsoft. PerceptionSimulation. Rotation3. Roll**</span><span class="sxs-lookup"><span data-stu-id="df69d-298">**Microsoft.PerceptionSimulation.Rotation3.Roll**</span></span>

<span data-ttu-id="df69d-299">Composant de roulement de la rotation, à droite autour de l’axe Z.</span><span class="sxs-lookup"><span data-stu-id="df69d-299">The Roll component of the Rotation, right around the Z axis.</span></span>

<span data-ttu-id="df69d-300">**Microsoft. PerceptionSimulation. Rotation3. #ctor (System. Single, System. Single, System. Single)**</span><span class="sxs-lookup"><span data-stu-id="df69d-300">**Microsoft.PerceptionSimulation.Rotation3.#ctor(System.Single,System.Single,System.Single)**</span></span>

<span data-ttu-id="df69d-301">Construisez un nouveau Rotation3.</span><span class="sxs-lookup"><span data-stu-id="df69d-301">Construct a new Rotation3.</span></span>

<span data-ttu-id="df69d-302">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-302">Parameters</span></span>
* <span data-ttu-id="df69d-303">tangage: composant de pas de la rotation.</span><span class="sxs-lookup"><span data-stu-id="df69d-303">pitch - The pitch component of the Rotation.</span></span>
* <span data-ttu-id="df69d-304">lacet: composant de lacet de la rotation.</span><span class="sxs-lookup"><span data-stu-id="df69d-304">yaw - The yaw component of the Rotation.</span></span>
* <span data-ttu-id="df69d-305">Roll-le composant Roll de la rotation.</span><span class="sxs-lookup"><span data-stu-id="df69d-305">roll - The roll component of the Rotation.</span></span>

### <a name="microsoftperceptionsimulationsimulatedhandjointconfiguration"></a><span data-ttu-id="df69d-306">Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration</span><span class="sxs-lookup"><span data-stu-id="df69d-306">Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration</span></span>

<span data-ttu-id="df69d-307">Décrit la configuration d’un joint sur une main simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-307">Describes the configuration of a joint on a simulated hand.</span></span>

```
public struct SimulatedHandJointConfiguration
{
    public Vector3 Position;
    public Rotation3 Rotation;
    public SimulatedHandJointTrackingAccuracy TrackingAccuracy;
}
```

<span data-ttu-id="df69d-308">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. position**</span><span class="sxs-lookup"><span data-stu-id="df69d-308">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Position**</span></span>

<span data-ttu-id="df69d-309">Position de la jointure.</span><span class="sxs-lookup"><span data-stu-id="df69d-309">The position of the joint.</span></span>

<span data-ttu-id="df69d-310">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. rotation**</span><span class="sxs-lookup"><span data-stu-id="df69d-310">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.Rotation**</span></span>

<span data-ttu-id="df69d-311">Rotation de la jointure.</span><span class="sxs-lookup"><span data-stu-id="df69d-311">The rotation of the joint.</span></span>

<span data-ttu-id="df69d-312">**Microsoft. PerceptionSimulation. SimulatedHandJointConfiguration. TrackingAccuracy**</span><span class="sxs-lookup"><span data-stu-id="df69d-312">**Microsoft.PerceptionSimulation.SimulatedHandJointConfiguration.TrackingAccuracy**</span></span>

<span data-ttu-id="df69d-313">Précision de suivi de la jointure.</span><span class="sxs-lookup"><span data-stu-id="df69d-313">The tracking accuracy of the joint.</span></span>


### <a name="microsoftperceptionsimulationfrustum"></a><span data-ttu-id="df69d-314">Microsoft. PerceptionSimulation. frustum</span><span class="sxs-lookup"><span data-stu-id="df69d-314">Microsoft.PerceptionSimulation.Frustum</span></span>

<span data-ttu-id="df69d-315">Décrit un frustum d’affichage, tel qu’il est généralement utilisé par un appareil photo.</span><span class="sxs-lookup"><span data-stu-id="df69d-315">Describes a view frustum, as typically used by a camera.</span></span>

```
public struct Frustum
{
    float Near;
    float Far;
    float FieldOfView;
    float AspectRatio;
}
```

<span data-ttu-id="df69d-316">**Microsoft. PerceptionSimulation. frustum. Near**</span><span class="sxs-lookup"><span data-stu-id="df69d-316">**Microsoft.PerceptionSimulation.Frustum.Near**</span></span>

<span data-ttu-id="df69d-317">Distance minimale contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="df69d-317">The minimum distance that is contained in the frustum.</span></span>

<span data-ttu-id="df69d-318">**Microsoft. PerceptionSimulation. frustum. Far**</span><span class="sxs-lookup"><span data-stu-id="df69d-318">**Microsoft.PerceptionSimulation.Frustum.Far**</span></span>

<span data-ttu-id="df69d-319">Distance maximale contenue dans le frustum.</span><span class="sxs-lookup"><span data-stu-id="df69d-319">The maximum distance that is contained in the frustum.</span></span>

<span data-ttu-id="df69d-320">**Microsoft. PerceptionSimulation. frustum. FieldOfView**</span><span class="sxs-lookup"><span data-stu-id="df69d-320">**Microsoft.PerceptionSimulation.Frustum.FieldOfView**</span></span>

<span data-ttu-id="df69d-321">Champ horizontal de la vue de frustum, en radians (inférieur à PI).</span><span class="sxs-lookup"><span data-stu-id="df69d-321">The horizontal field of view of the frustum, in radians (less than PI).</span></span>

<span data-ttu-id="df69d-322">**Microsoft. PerceptionSimulation. frustum. AspectRatio**</span><span class="sxs-lookup"><span data-stu-id="df69d-322">**Microsoft.PerceptionSimulation.Frustum.AspectRatio**</span></span>

<span data-ttu-id="df69d-323">Rapport entre le champ horizontal de la vue et le champ vertical de l’affichage.</span><span class="sxs-lookup"><span data-stu-id="df69d-323">The ratio of horizontal field of view to vertical field of view.</span></span>

### <a name="microsoftperceptionsimulationiperceptionsimulationmanager"></a><span data-ttu-id="df69d-324">Microsoft. PerceptionSimulation. IPerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="df69d-324">Microsoft.PerceptionSimulation.IPerceptionSimulationManager</span></span>

<span data-ttu-id="df69d-325">Racine pour la génération des paquets utilisés pour contrôler un appareil.</span><span class="sxs-lookup"><span data-stu-id="df69d-325">Root for generating the packets used to control a device.</span></span>

```
public interface IPerceptionSimulationManager
{   
    ISimulatedDevice Device { get; }
    ISimulatedHuman Human { get; }
    void Reset();
}
```

<span data-ttu-id="df69d-326">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Device**</span><span class="sxs-lookup"><span data-stu-id="df69d-326">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Device**</span></span>

<span data-ttu-id="df69d-327">Récupérez l’objet d’appareil simulé qui interprète l’homme simulé et le monde simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-327">Retrieve the simulated device object that interprets the simulated human and the simulated world.</span></span>

<span data-ttu-id="df69d-328">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Human**</span><span class="sxs-lookup"><span data-stu-id="df69d-328">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Human**</span></span>

<span data-ttu-id="df69d-329">Récupérez l’objet qui contrôle l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-329">Retrieve the object that controls the simulated human.</span></span>

<span data-ttu-id="df69d-330">**Microsoft. PerceptionSimulation. IPerceptionSimulationManager. Reset**</span><span class="sxs-lookup"><span data-stu-id="df69d-330">**Microsoft.PerceptionSimulation.IPerceptionSimulationManager.Reset**</span></span>

<span data-ttu-id="df69d-331">Rétablit l’État par défaut de la simulation.</span><span class="sxs-lookup"><span data-stu-id="df69d-331">Resets the simulation to its default state.</span></span>

### <a name="microsoftperceptionsimulationisimulateddevice"></a><span data-ttu-id="df69d-332">Microsoft. PerceptionSimulation. ISimulatedDevice</span><span class="sxs-lookup"><span data-stu-id="df69d-332">Microsoft.PerceptionSimulation.ISimulatedDevice</span></span>

<span data-ttu-id="df69d-333">Interface décrivant l’appareil qui interprète le monde simulé et l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-333">Interface describing the device which interprets the simulated world and the simulated human</span></span>

```
public interface ISimulatedDevice
{
    ISimulatedHeadTracker HeadTracker { get; }
    ISimulatedHandTracker HandTracker { get; }
    void SetSimulatedDeviceType(SimulatedDeviceType type);
}
```

<span data-ttu-id="df69d-334">**Microsoft. PerceptionSimulation. ISimulatedDevice. HeadTracker**</span><span class="sxs-lookup"><span data-stu-id="df69d-334">**Microsoft.PerceptionSimulation.ISimulatedDevice.HeadTracker**</span></span>

<span data-ttu-id="df69d-335">Récupérez le dispositif de suivi des têtes à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-335">Retrieve the Head Tracker from the Simulated Device.</span></span>

<span data-ttu-id="df69d-336">**Microsoft. PerceptionSimulation. ISimulatedDevice. HandTracker**</span><span class="sxs-lookup"><span data-stu-id="df69d-336">**Microsoft.PerceptionSimulation.ISimulatedDevice.HandTracker**</span></span>

<span data-ttu-id="df69d-337">Récupérez le dispositif de suivi de main à partir de l’appareil simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-337">Retrieve the Hand Tracker from the Simulated Device.</span></span>

<span data-ttu-id="df69d-338">**Microsoft. PerceptionSimulation. ISimulatedDevice. SetSimulatedDeviceType (Microsoft. PerceptionSimulation. SimulatedDeviceType)**</span><span class="sxs-lookup"><span data-stu-id="df69d-338">**Microsoft.PerceptionSimulation.ISimulatedDevice.SetSimulatedDeviceType(Microsoft.PerceptionSimulation.SimulatedDeviceType)**</span></span>

<span data-ttu-id="df69d-339">Définissez les propriétés de l’appareil simulé pour qu’elles correspondent au type d’appareil fourni.</span><span class="sxs-lookup"><span data-stu-id="df69d-339">Set the properties of the simulated device to match the provided device type.</span></span>

<span data-ttu-id="df69d-340">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-340">Parameters</span></span>
* <span data-ttu-id="df69d-341">type-le nouveau type d’appareil simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-341">type - The new type of Simulated Device</span></span>

### <a name="microsoftperceptionsimulationisimulatedheadtracker"></a><span data-ttu-id="df69d-342">Microsoft. PerceptionSimulation. ISimulatedHeadTracker</span><span class="sxs-lookup"><span data-stu-id="df69d-342">Microsoft.PerceptionSimulation.ISimulatedHeadTracker</span></span>

<span data-ttu-id="df69d-343">Interface décrivant la partie de l’appareil simulé qui effectue le suivi du chef de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-343">Interface describing the portion of the simulated device that tracks the head of the simulated human.</span></span>

```
public interface ISimulatedHeadTracker
{
    HeadTrackerMode HeadTrackerMode { get; set; }
};
```

<span data-ttu-id="df69d-344">**Microsoft. PerceptionSimulation. ISimulatedHeadTracker. HeadTrackerMode**</span><span class="sxs-lookup"><span data-stu-id="df69d-344">**Microsoft.PerceptionSimulation.ISimulatedHeadTracker.HeadTrackerMode**</span></span>

<span data-ttu-id="df69d-345">Récupère et définit le mode de suivi d’en-tête actuel.</span><span class="sxs-lookup"><span data-stu-id="df69d-345">Retrieves and sets the current head tracker mode.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhandtracker"></a><span data-ttu-id="df69d-346">Microsoft. PerceptionSimulation. ISimulatedHandTracker</span><span class="sxs-lookup"><span data-stu-id="df69d-346">Microsoft.PerceptionSimulation.ISimulatedHandTracker</span></span>

<span data-ttu-id="df69d-347">Interface décrivant la partie de l’appareil simulé qui effectue le suivi des mains de l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-347">Interface describing the portion of the simulated device that tracks the hands of the simulated human</span></span>

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

<span data-ttu-id="df69d-348">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-348">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.WorldPosition**</span></span>

<span data-ttu-id="df69d-349">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-349">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="df69d-350">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. position**</span><span class="sxs-lookup"><span data-stu-id="df69d-350">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Position**</span></span>

<span data-ttu-id="df69d-351">Récupère et définit la position du suivi de la main simulé, par rapport au centre de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="df69d-351">Retrieve and set the position of the simulated hand tracker, relative to the center of the head.</span></span>

<span data-ttu-id="df69d-352">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. brai**</span><span class="sxs-lookup"><span data-stu-id="df69d-352">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Pitch**</span></span>

<span data-ttu-id="df69d-353">Récupérer et définir le pas à pas bas du suivi simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-353">Retrieve and set the downward pitch of the simulated hand tracker.</span></span>

<span data-ttu-id="df69d-354">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. FrustumIgnored**</span><span class="sxs-lookup"><span data-stu-id="df69d-354">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.FrustumIgnored**</span></span>

<span data-ttu-id="df69d-355">Récupérez et définissez si le frustum du suivi de la main simulé est ignoré.</span><span class="sxs-lookup"><span data-stu-id="df69d-355">Retrieve and set whether the frustum of the simulated hand tracker is ignored.</span></span> <span data-ttu-id="df69d-356">Lorsqu’ils sont ignorés, les deux mains sont toujours visibles.</span><span class="sxs-lookup"><span data-stu-id="df69d-356">When ignored, both hands are always visible.</span></span> <span data-ttu-id="df69d-357">Lorsqu’elles ne sont pas ignorées (par défaut), elles ne sont visibles que lorsqu’elles se trouvent dans le frustum du dispositif de suivi de la main.</span><span class="sxs-lookup"><span data-stu-id="df69d-357">When not ignored (the default) hands are only visible when they are within the frustum of the hand tracker.</span></span>

<span data-ttu-id="df69d-358">**Microsoft. PerceptionSimulation. ISimulatedHandTracker. frustum**</span><span class="sxs-lookup"><span data-stu-id="df69d-358">**Microsoft.PerceptionSimulation.ISimulatedHandTracker.Frustum**</span></span>

<span data-ttu-id="df69d-359">Récupérez et définissez les propriétés frustum utilisées pour déterminer si les mains sont visibles pour le suivi de la main simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-359">Retrieve and set the frustum properties used to determine if hands are visible to the simulated hand tracker.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman"></a><span data-ttu-id="df69d-360">Microsoft. PerceptionSimulation. ISimulatedHuman</span><span class="sxs-lookup"><span data-stu-id="df69d-360">Microsoft.PerceptionSimulation.ISimulatedHuman</span></span>

<span data-ttu-id="df69d-361">Interface de niveau supérieur pour le contrôle de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-361">Top level interface for controlling the simulated human.</span></span>

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

<span data-ttu-id="df69d-362">**Microsoft. PerceptionSimulation. ISimulatedHuman. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-362">**Microsoft.PerceptionSimulation.ISimulatedHuman.WorldPosition**</span></span>

<span data-ttu-id="df69d-363">Récupérer et définir la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-363">Retrieve and set the position of the node with relation to the world, in meters.</span></span> <span data-ttu-id="df69d-364">La position correspond à un point au centre des pieds de l’homme.</span><span class="sxs-lookup"><span data-stu-id="df69d-364">The position corresponds to a point at the center of the human's feet.</span></span>

<span data-ttu-id="df69d-365">**Microsoft. PerceptionSimulation. ISimulatedHuman. direction**</span><span class="sxs-lookup"><span data-stu-id="df69d-365">**Microsoft.PerceptionSimulation.ISimulatedHuman.Direction**</span></span>

<span data-ttu-id="df69d-366">Récupérez et définissez le sens des visages humains simulés dans le monde.</span><span class="sxs-lookup"><span data-stu-id="df69d-366">Retrieve and set the direction the simulated human faces in the world.</span></span> <span data-ttu-id="df69d-367">0 radians est confronté à l’axe Z négatif.</span><span class="sxs-lookup"><span data-stu-id="df69d-367">0 radians faces down the negative Z axis.</span></span> <span data-ttu-id="df69d-368">Les radians positifs pivotent dans le sens des aiguilles d’une montre autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="df69d-368">Positive radians rotate clockwise about the Y axis.</span></span>

<span data-ttu-id="df69d-369">**Microsoft. PerceptionSimulation. ISimulatedHuman. Height**</span><span class="sxs-lookup"><span data-stu-id="df69d-369">**Microsoft.PerceptionSimulation.ISimulatedHuman.Height**</span></span>

<span data-ttu-id="df69d-370">Récupérez et définissez la hauteur de l’homme simulé, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-370">Retrieve and set the height of the simulated human, in meters.</span></span>

<span data-ttu-id="df69d-371">**Microsoft. PerceptionSimulation. ISimulatedHuman. LeftHand**</span><span class="sxs-lookup"><span data-stu-id="df69d-371">**Microsoft.PerceptionSimulation.ISimulatedHuman.LeftHand**</span></span>

<span data-ttu-id="df69d-372">Récupérez la main gauche de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-372">Retrieve the left hand of the simulated human.</span></span>

<span data-ttu-id="df69d-373">**Microsoft. PerceptionSimulation. ISimulatedHuman. à droite**</span><span class="sxs-lookup"><span data-stu-id="df69d-373">**Microsoft.PerceptionSimulation.ISimulatedHuman.RightHand**</span></span>

<span data-ttu-id="df69d-374">Récupérez la main droite de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-374">Retrieve the right hand of the simulated human.</span></span>

<span data-ttu-id="df69d-375">**Microsoft. PerceptionSimulation. ISimulatedHuman. Head**</span><span class="sxs-lookup"><span data-stu-id="df69d-375">**Microsoft.PerceptionSimulation.ISimulatedHuman.Head**</span></span>

<span data-ttu-id="df69d-376">Récupérez l’en-tête de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-376">Retrieve the head of the simulated human.</span></span>

<span data-ttu-id="df69d-377">**Microsoft. PerceptionSimulation. ISimulatedHuman. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="df69d-377">**Microsoft.PerceptionSimulation.ISimulatedHuman.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="df69d-378">Déplacer le humain simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-378">Move the simulated human relative to its current position, in meters.</span></span>

<span data-ttu-id="df69d-379">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-379">Parameters</span></span>
* <span data-ttu-id="df69d-380">translation: translation à déplacer, par rapport à la position actuelle.</span><span class="sxs-lookup"><span data-stu-id="df69d-380">translation - The translation to move, relative to current position.</span></span>

<span data-ttu-id="df69d-381">**Microsoft. PerceptionSimulation. ISimulatedHuman. Rotate (System. Single)**</span><span class="sxs-lookup"><span data-stu-id="df69d-381">**Microsoft.PerceptionSimulation.ISimulatedHuman.Rotate(System.Single)**</span></span>

<span data-ttu-id="df69d-382">Faire pivoter l’homme simulé par rapport à sa direction actuelle, dans le sens des aiguilles d’une montre autour de l’axe Y</span><span class="sxs-lookup"><span data-stu-id="df69d-382">Rotate the simulated human relative to its current direction, clockwise about the Y axis</span></span>

<span data-ttu-id="df69d-383">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-383">Parameters</span></span>
* <span data-ttu-id="df69d-384">radians-la valeur de rotation autour de l’axe Y.</span><span class="sxs-lookup"><span data-stu-id="df69d-384">radians - The amount to rotate around the Y axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhuman2"></a><span data-ttu-id="df69d-385">Microsoft. PerceptionSimulation. ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="df69d-385">Microsoft.PerceptionSimulation.ISimulatedHuman2</span></span>

<span data-ttu-id="df69d-386">Des propriétés supplémentaires sont disponibles en convertissant le ISimulatedHuman en ISimulatedHuman2</span><span class="sxs-lookup"><span data-stu-id="df69d-386">Additional properties are available by casting the ISimulatedHuman to ISimulatedHuman2</span></span>

```
public interface ISimulatedHuman2
{
    /* New members in addition to those available on ISimulatedHuman */
    ISimulatedSixDofController LeftController { get; }
    ISimulatedSixDofController RightController { get; }
}
```

<span data-ttu-id="df69d-387">**Microsoft. PerceptionSimulation. ISimulatedHuman2. LeftController**</span><span class="sxs-lookup"><span data-stu-id="df69d-387">**Microsoft.PerceptionSimulation.ISimulatedHuman2.LeftController**</span></span>

<span data-ttu-id="df69d-388">Récupérez le contrôleur 6-DDL de gauche.</span><span class="sxs-lookup"><span data-stu-id="df69d-388">Retrieve the left 6-DOF controller.</span></span>

<span data-ttu-id="df69d-389">**Microsoft. PerceptionSimulation. ISimulatedHuman2. RightController**</span><span class="sxs-lookup"><span data-stu-id="df69d-389">**Microsoft.PerceptionSimulation.ISimulatedHuman2.RightController**</span></span>

<span data-ttu-id="df69d-390">Récupérez le contrôleur 6-DDL approprié.</span><span class="sxs-lookup"><span data-stu-id="df69d-390">Retrieve the right 6-DOF controller.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhand"></a><span data-ttu-id="df69d-391">Microsoft. PerceptionSimulation. ISimulatedHand</span><span class="sxs-lookup"><span data-stu-id="df69d-391">Microsoft.PerceptionSimulation.ISimulatedHand</span></span>

<span data-ttu-id="df69d-392">Interface décrivant une main de l’homme simulé</span><span class="sxs-lookup"><span data-stu-id="df69d-392">Interface describing a hand of the simulated human</span></span>

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

<span data-ttu-id="df69d-393">**Microsoft. PerceptionSimulation. ISimulatedHand. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-393">**Microsoft.PerceptionSimulation.ISimulatedHand.WorldPosition**</span></span>

<span data-ttu-id="df69d-394">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-394">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="df69d-395">**Microsoft. PerceptionSimulation. ISimulatedHand. position**</span><span class="sxs-lookup"><span data-stu-id="df69d-395">**Microsoft.PerceptionSimulation.ISimulatedHand.Position**</span></span>

<span data-ttu-id="df69d-396">Récupérer et définir la position de la main simulée par rapport à l’homme, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-396">Retrieve and set the position of the simulated hand relative to the human, in meters.</span></span>

<span data-ttu-id="df69d-397">**Microsoft. PerceptionSimulation. ISimulatedHand. Activated**</span><span class="sxs-lookup"><span data-stu-id="df69d-397">**Microsoft.PerceptionSimulation.ISimulatedHand.Activated**</span></span>

<span data-ttu-id="df69d-398">Récupère et définit si la main est actuellement activée.</span><span class="sxs-lookup"><span data-stu-id="df69d-398">Retrieve and set whether the hand is currently activated.</span></span>

<span data-ttu-id="df69d-399">**Microsoft. PerceptionSimulation. ISimulatedHand. visible**</span><span class="sxs-lookup"><span data-stu-id="df69d-399">**Microsoft.PerceptionSimulation.ISimulatedHand.Visible**</span></span>

<span data-ttu-id="df69d-400">Récupère si la main est actuellement visible pour le SimulatedDevice (IE, si elle se trouve dans une position à détecter par le HandTracker).</span><span class="sxs-lookup"><span data-stu-id="df69d-400">Retrieve whether the hand is currently visible to the SimulatedDevice (ie, whether it's in a position to be detected by the HandTracker).</span></span>

<span data-ttu-id="df69d-401">**Microsoft. PerceptionSimulation. ISimulatedHand. EnsureVisible**</span><span class="sxs-lookup"><span data-stu-id="df69d-401">**Microsoft.PerceptionSimulation.ISimulatedHand.EnsureVisible**</span></span>

<span data-ttu-id="df69d-402">Déplacez la main de manière à ce qu’elle soit visible par le SimulatedDevice.</span><span class="sxs-lookup"><span data-stu-id="df69d-402">Move the hand such that it is visible to the SimulatedDevice.</span></span>

<span data-ttu-id="df69d-403">**Microsoft. PerceptionSimulation. ISimulatedHand. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="df69d-403">**Microsoft.PerceptionSimulation.ISimulatedHand.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="df69d-404">Déplacer la position de la main simulée par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-404">Move the position of the simulated hand relative to its current position, in meters.</span></span>

<span data-ttu-id="df69d-405">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-405">Parameters</span></span>
* <span data-ttu-id="df69d-406">translation-le montant pour traduire la main simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-406">translation - The amount to translate the simulated hand.</span></span>

<span data-ttu-id="df69d-407">**Microsoft. PerceptionSimulation. ISimulatedHand. PerformGesture (Microsoft. PerceptionSimulation. SimulatedGesture)**</span><span class="sxs-lookup"><span data-stu-id="df69d-407">**Microsoft.PerceptionSimulation.ISimulatedHand.PerformGesture(Microsoft.PerceptionSimulation.SimulatedGesture)**</span></span>

<span data-ttu-id="df69d-408">Effectuez un mouvement à l’aide de la main simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-408">Perform a gesture using the simulated hand.</span></span>  <span data-ttu-id="df69d-409">Elle sera détectée uniquement par le système si la main est activée.</span><span class="sxs-lookup"><span data-stu-id="df69d-409">It will only be detected by the system if the hand is enabled.</span></span>

<span data-ttu-id="df69d-410">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-410">Parameters</span></span>
* <span data-ttu-id="df69d-411">geste: mouvement à effectuer.</span><span class="sxs-lookup"><span data-stu-id="df69d-411">gesture - The gesture to perform.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand2"></a><span data-ttu-id="df69d-412">Microsoft. PerceptionSimulation. ISimulatedHand2</span><span class="sxs-lookup"><span data-stu-id="df69d-412">Microsoft.PerceptionSimulation.ISimulatedHand2</span></span>

<span data-ttu-id="df69d-413">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand2.</span><span class="sxs-lookup"><span data-stu-id="df69d-413">Additional properties are available by casting an ISimulatedHand to ISimulatedHand2.</span></span>
```
public interface ISimulatedHand2
{
    /* New members in addition to those available on ISimulatedHand */
    Rotation3 Orientation { get; set; }
}
```

<span data-ttu-id="df69d-414">**Microsoft. PerceptionSimulation. ISimulatedHand2. orientation**</span><span class="sxs-lookup"><span data-stu-id="df69d-414">**Microsoft.PerceptionSimulation.ISimulatedHand2.Orientation**</span></span>

<span data-ttu-id="df69d-415">Récupère ou définit la rotation de la main simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-415">Retrieve or set the rotation of the simulated hand.</span></span>  <span data-ttu-id="df69d-416">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="df69d-416">Positive radians rotate clockwise when looking along the axis.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhand3"></a><span data-ttu-id="df69d-417">Microsoft. PerceptionSimulation. ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="df69d-417">Microsoft.PerceptionSimulation.ISimulatedHand3</span></span>

<span data-ttu-id="df69d-418">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHand en ISimulatedHand3</span><span class="sxs-lookup"><span data-stu-id="df69d-418">Additional properties are available by casting an ISimulatedHand to ISimulatedHand3</span></span>
```
public interface ISimulatedHand3
{
    /* New members in addition to those available on ISimulatedHand and ISimulatedHand2 */
    GetJointConfiguration(SimulatedHandJoint joint, out SimulatedHandJointConfiguration jointConfiguration);
    SetJointConfiguration(SimulatedHandJoint joint, SimulatedHandJointConfiguration jointConfiguration);
    SetHandPose(SimulatedHandPose pose, bool animate);
}
```

<span data-ttu-id="df69d-419">**Microsoft. PerceptionSimulation. ISimulatedHand3. GetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="df69d-419">**Microsoft.PerceptionSimulation.ISimulatedHand3.GetJointConfiguration**</span></span>

<span data-ttu-id="df69d-420">Obtient la configuration conjointe pour l’articulation spécifiée.</span><span class="sxs-lookup"><span data-stu-id="df69d-420">Get the joint configuration for the specified joint.</span></span>

<span data-ttu-id="df69d-421">**Microsoft. PerceptionSimulation. ISimulatedHand3. SetJointConfiguration**</span><span class="sxs-lookup"><span data-stu-id="df69d-421">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetJointConfiguration**</span></span>

<span data-ttu-id="df69d-422">Définit la configuration conjointe pour l’articulation spécifiée.</span><span class="sxs-lookup"><span data-stu-id="df69d-422">Set the joint configuration for the specified joint.</span></span>

<span data-ttu-id="df69d-423">**Microsoft. PerceptionSimulation. ISimulatedHand3. SetHandPose**</span><span class="sxs-lookup"><span data-stu-id="df69d-423">**Microsoft.PerceptionSimulation.ISimulatedHand3.SetHandPose**</span></span>

<span data-ttu-id="df69d-424">Définissez la main sur une pose connue avec un indicateur facultatif à animer.</span><span class="sxs-lookup"><span data-stu-id="df69d-424">Set the hand to a known pose with an optional flag to animate.</span></span>  <span data-ttu-id="df69d-425">Remarque: l’animation ne permettra pas aux jointures de refléter immédiatement leurs configurations conjointes finales.</span><span class="sxs-lookup"><span data-stu-id="df69d-425">Note: animating won't result in joints immediately reflecting their final joint configurations.</span></span>


### <a name="microsoftperceptionsimulationisimulatedhead"></a><span data-ttu-id="df69d-426">Microsoft. PerceptionSimulation. ISimulatedHead</span><span class="sxs-lookup"><span data-stu-id="df69d-426">Microsoft.PerceptionSimulation.ISimulatedHead</span></span>

<span data-ttu-id="df69d-427">Interface décrivant l’en-tête de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-427">Interface describing the head of the simulated human.</span></span>

```
public interface ISimulatedHead
{
    Vector3 WorldPosition { get; }
    Rotation3 Rotation { get; set; }
    float Diameter { get; set; }
    void Rotate(Rotation3 rotation);
}
```

<span data-ttu-id="df69d-428">**Microsoft. PerceptionSimulation. ISimulatedHead. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-428">**Microsoft.PerceptionSimulation.ISimulatedHead.WorldPosition**</span></span>

<span data-ttu-id="df69d-429">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-429">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="df69d-430">**Microsoft. PerceptionSimulation. ISimulatedHead. rotation**</span><span class="sxs-lookup"><span data-stu-id="df69d-430">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotation**</span></span>

<span data-ttu-id="df69d-431">Récupère la rotation de la tête simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-431">Retrieve the rotation of the simulated head.</span></span> <span data-ttu-id="df69d-432">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="df69d-432">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="df69d-433">**Microsoft. PerceptionSimulation. ISimulatedHead. diametre**</span><span class="sxs-lookup"><span data-stu-id="df69d-433">**Microsoft.PerceptionSimulation.ISimulatedHead.Diameter**</span></span>

<span data-ttu-id="df69d-434">Récupérer le diamètre de la tête simulée.</span><span class="sxs-lookup"><span data-stu-id="df69d-434">Retrieve the simulated head's diameter.</span></span> <span data-ttu-id="df69d-435">Cette valeur est utilisée pour déterminer le centre de l’en-tête (point de rotation).</span><span class="sxs-lookup"><span data-stu-id="df69d-435">This value is used to determine the head's center (point of rotation).</span></span>

<span data-ttu-id="df69d-436">**Microsoft. PerceptionSimulation. ISimulatedHead. Rotate (Microsoft. PerceptionSimulation. Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="df69d-436">**Microsoft.PerceptionSimulation.ISimulatedHead.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="df69d-437">Faire pivoter la tête simulée par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="df69d-437">Rotate the simulated head relative to its current rotation.</span></span> <span data-ttu-id="df69d-438">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="df69d-438">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="df69d-439">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-439">Parameters</span></span>
* <span data-ttu-id="df69d-440">rotation: quantité à faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="df69d-440">rotation - The amount to rotate.</span></span>

### <a name="microsoftperceptionsimulationisimulatedhead2"></a><span data-ttu-id="df69d-441">Microsoft. PerceptionSimulation. ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="df69d-441">Microsoft.PerceptionSimulation.ISimulatedHead2</span></span>

<span data-ttu-id="df69d-442">Des propriétés supplémentaires sont disponibles en convertissant un ISimulatedHead en ISimulatedHead2</span><span class="sxs-lookup"><span data-stu-id="df69d-442">Additional properties are available by casting an ISimulatedHead to ISimulatedHead2</span></span>

```
public interface ISimulatedHead2
{
    /* New members in addition to those available on ISimulatedHead */
    ISimulatedEyes Eyes { get; }
}
```

<span data-ttu-id="df69d-443">**Microsoft. PerceptionSimulation. ISimulatedHead2. Eyes**</span><span class="sxs-lookup"><span data-stu-id="df69d-443">**Microsoft.PerceptionSimulation.ISimulatedHead2.Eyes**</span></span>

<span data-ttu-id="df69d-444">Récupérez les yeux de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-444">Retrieve the eyes of the simulated human.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller"></a><span data-ttu-id="df69d-445">Microsoft. PerceptionSimulation. ISimulatedSixDofController</span><span class="sxs-lookup"><span data-stu-id="df69d-445">Microsoft.PerceptionSimulation.ISimulatedSixDofController</span></span>

<span data-ttu-id="df69d-446">Interface décrivant un contrôleur 6-DDL associé à l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-446">Interface describing a 6-DOF controller associated with the simulated human.</span></span>

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

<span data-ttu-id="df69d-447">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-447">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.WorldPosition**</span></span>

<span data-ttu-id="df69d-448">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-448">Retrieve the position of the node with relation to the world, in meters.</span></span>

<span data-ttu-id="df69d-449">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Status**</span><span class="sxs-lookup"><span data-stu-id="df69d-449">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Status**</span></span>

<span data-ttu-id="df69d-450">Récupère ou définit l’état actuel du contrôleur.</span><span class="sxs-lookup"><span data-stu-id="df69d-450">Retrieve or set the current state of the controller.</span></span>  <span data-ttu-id="df69d-451">L’état du contrôleur doit être défini sur une valeur autre que OFF avant que les appels au déplacement, à la rotation ou à l’appui sur les boutons échouent.</span><span class="sxs-lookup"><span data-stu-id="df69d-451">The controller status must be set to a value other than Off before any calls to move, rotate or press buttons will succeed.</span></span>

<span data-ttu-id="df69d-452">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. position**</span><span class="sxs-lookup"><span data-stu-id="df69d-452">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Position**</span></span>

<span data-ttu-id="df69d-453">Récupérez ou définissez la position du contrôleur simulé par rapport à l’homme, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-453">Retrieve or set the position of the simulated controller relative to the human, in meters.</span></span>

<span data-ttu-id="df69d-454">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. orientation**</span><span class="sxs-lookup"><span data-stu-id="df69d-454">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Orientation**</span></span>

<span data-ttu-id="df69d-455">Récupérer ou définir l’orientation du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-455">Retrieve or set the orientation of the simulated controller.</span></span>

<span data-ttu-id="df69d-456">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. Move (Microsoft. PerceptionSimulation. Vector3)**</span><span class="sxs-lookup"><span data-stu-id="df69d-456">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.Move(Microsoft.PerceptionSimulation.Vector3)**</span></span>

<span data-ttu-id="df69d-457">Déplacer la position du contrôleur simulé par rapport à sa position actuelle, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-457">Move the position of the simulated controller relative to its current position, in meters.</span></span>

<span data-ttu-id="df69d-458">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-458">Parameters</span></span>
* <span data-ttu-id="df69d-459">Traduction: quantité de conversion du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-459">translation - The amount to translate the simulated controller.</span></span>

<span data-ttu-id="df69d-460">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. PressButton (SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="df69d-460">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.PressButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="df69d-461">Appuyez sur un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-461">Press a button on the simulated controller.</span></span>  <span data-ttu-id="df69d-462">Il ne sera détecté par le système que si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="df69d-462">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="df69d-463">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-463">Parameters</span></span>
* <span data-ttu-id="df69d-464">Button-bouton sur lequel appuyer.</span><span class="sxs-lookup"><span data-stu-id="df69d-464">button - The button to press.</span></span>

<span data-ttu-id="df69d-465">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. ReleaseButton (SimulatedSixDofControllerButton)**</span><span class="sxs-lookup"><span data-stu-id="df69d-465">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.ReleaseButton(SimulatedSixDofControllerButton)**</span></span>

<span data-ttu-id="df69d-466">Publiez un bouton sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-466">Release a button on the simulated controller.</span></span>  <span data-ttu-id="df69d-467">Il ne sera détecté par le système que si le contrôleur est activé.</span><span class="sxs-lookup"><span data-stu-id="df69d-467">It will only be detected by the system if the controller is enabled.</span></span>

<span data-ttu-id="df69d-468">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-468">Parameters</span></span>
* <span data-ttu-id="df69d-469">Button-bouton à libérer.</span><span class="sxs-lookup"><span data-stu-id="df69d-469">button - The button to release.</span></span>

<span data-ttu-id="df69d-470">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. GetTouchpadPosition (sortie float, out float)**</span><span class="sxs-lookup"><span data-stu-id="df69d-470">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.GetTouchpadPosition(out float, out float)**</span></span>

<span data-ttu-id="df69d-471">Obtient la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-471">Get the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="df69d-472">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-472">Parameters</span></span>
* <span data-ttu-id="df69d-473">x-la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-473">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="df69d-474">y: position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-474">y - The vertical position of the finger.</span></span>

<span data-ttu-id="df69d-475">**Microsoft. PerceptionSimulation. ISimulatedSixDofController. SetTouchpadPosition (float, float)**</span><span class="sxs-lookup"><span data-stu-id="df69d-475">**Microsoft.PerceptionSimulation.ISimulatedSixDofController.SetTouchpadPosition(float, float)**</span></span>

<span data-ttu-id="df69d-476">Définit la position d’un doigt simulé sur le pavé tactile du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-476">Set the position of a simulated finger on the simulated controller's touchpad.</span></span>

<span data-ttu-id="df69d-477">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-477">Parameters</span></span>
* <span data-ttu-id="df69d-478">x-la position horizontale du doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-478">x - The horizontal position of the finger.</span></span>
* <span data-ttu-id="df69d-479">y: position verticale du doigt.</span><span class="sxs-lookup"><span data-stu-id="df69d-479">y - The vertical position of the finger.</span></span>

### <a name="microsoftperceptionsimulationisimulatedsixdofcontroller2"></a><span data-ttu-id="df69d-480">Microsoft. PerceptionSimulation. ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="df69d-480">Microsoft.PerceptionSimulation.ISimulatedSixDofController2</span></span>

<span data-ttu-id="df69d-481">Des propriétés et méthodes supplémentaires sont disponibles en convertissant un ISimulatedSixDofController en ISimulatedSixDofController2</span><span class="sxs-lookup"><span data-stu-id="df69d-481">Additional properties and methods are available by casting an ISimulatedSixDofController to ISimulatedSixDofController2</span></span>

```
public interface ISimulatedSixDofController2
{
    /* New members in addition to those available on ISimulatedSixDofController */
    void GetThumbstickPosition(out float x, out float y);
    void SetThumbstickPosition(float x, float y);
    float BatteryLevel { get; set; }
}
```

<span data-ttu-id="df69d-482">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. GetThumbstickPosition (sortie float, out float)**</span><span class="sxs-lookup"><span data-stu-id="df69d-482">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.GetThumbstickPosition(out float, out float)**</span></span>

<span data-ttu-id="df69d-483">Obtient la position du stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-483">Get the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="df69d-484">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-484">Parameters</span></span>
* <span data-ttu-id="df69d-485">x-la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="df69d-485">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="df69d-486">y: position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="df69d-486">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="df69d-487">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. SetThumbstickPosition (float, float)**</span><span class="sxs-lookup"><span data-stu-id="df69d-487">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.SetThumbstickPosition(float, float)**</span></span>

<span data-ttu-id="df69d-488">Définissez la position du stick analogique simulé sur le contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-488">Set the position of the simulated thumbstick on the simulated controller.</span></span>

<span data-ttu-id="df69d-489">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-489">Parameters</span></span>
* <span data-ttu-id="df69d-490">x-la position horizontale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="df69d-490">x - The horizontal position of the thumbstick.</span></span>
* <span data-ttu-id="df69d-491">y: position verticale du stick analogique.</span><span class="sxs-lookup"><span data-stu-id="df69d-491">y - The vertical position of the thumbstick.</span></span>

<span data-ttu-id="df69d-492">**Microsoft. PerceptionSimulation. ISimulatedSixDofController2. BatteryLevel**</span><span class="sxs-lookup"><span data-stu-id="df69d-492">**Microsoft.PerceptionSimulation.ISimulatedSixDofController2.BatteryLevel**</span></span>

<span data-ttu-id="df69d-493">Récupérez ou définissez le niveau de batterie du contrôleur simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-493">Retrieve or set the battery level of the simulated controller.</span></span>  <span data-ttu-id="df69d-494">La valeur doit être supérieure à 0,0 et inférieure ou égale à 100,0.</span><span class="sxs-lookup"><span data-stu-id="df69d-494">The value must be greater than 0.0 and less than or equal to 100.0.</span></span>


### <a name="microsoftperceptionsimulationisimulatedeyes"></a><span data-ttu-id="df69d-495">Microsoft. PerceptionSimulation. ISimulatedEyes</span><span class="sxs-lookup"><span data-stu-id="df69d-495">Microsoft.PerceptionSimulation.ISimulatedEyes</span></span>

<span data-ttu-id="df69d-496">Interface décrivant les yeux de l’homme simulé.</span><span class="sxs-lookup"><span data-stu-id="df69d-496">Interface describing the eyes of the simulated human.</span></span>

```
public interface ISimulatedEyes
{
    Rotation3 Rotation { get; set; }
    void Rotate(Rotation3 rotation);
    SimulatedEyesCalibrationState CalibrationState { get; set; }
    Vector3 WorldPosition { get; }
}
```

<span data-ttu-id="df69d-497">**Microsoft. PerceptionSimulation. ISimulatedEyes. rotation**</span><span class="sxs-lookup"><span data-stu-id="df69d-497">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotation**</span></span>

<span data-ttu-id="df69d-498">Récupérer la rotation des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="df69d-498">Retrieve the rotation of the simulated eyes.</span></span> <span data-ttu-id="df69d-499">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="df69d-499">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="df69d-500">**Microsoft. PerceptionSimulation. ISimulatedEyes. Rotate (Microsoft. PerceptionSimulation. Rotation3)**</span><span class="sxs-lookup"><span data-stu-id="df69d-500">**Microsoft.PerceptionSimulation.ISimulatedEyes.Rotate(Microsoft.PerceptionSimulation.Rotation3)**</span></span>

<span data-ttu-id="df69d-501">Faire pivoter les yeux simulés par rapport à sa rotation actuelle.</span><span class="sxs-lookup"><span data-stu-id="df69d-501">Rotate the simulated eyes relative to its current rotation.</span></span> <span data-ttu-id="df69d-502">Les radians positifs pivotent dans le sens des aiguilles d’une montre sur l’axe.</span><span class="sxs-lookup"><span data-stu-id="df69d-502">Positive radians rotate clockwise when looking along the axis.</span></span>

<span data-ttu-id="df69d-503">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-503">Parameters</span></span>
* <span data-ttu-id="df69d-504">rotation: quantité à faire pivoter.</span><span class="sxs-lookup"><span data-stu-id="df69d-504">rotation - The amount to rotate.</span></span>

<span data-ttu-id="df69d-505">**Microsoft. PerceptionSimulation. ISimulatedEyes. CalibrationState**</span><span class="sxs-lookup"><span data-stu-id="df69d-505">**Microsoft.PerceptionSimulation.ISimulatedEyes.CalibrationState**</span></span>

<span data-ttu-id="df69d-506">Récupère ou définit l’état d’étalonnage des yeux simulés.</span><span class="sxs-lookup"><span data-stu-id="df69d-506">Retrieves or sets the calibration state of the simulated eyes.</span></span>

<span data-ttu-id="df69d-507">**Microsoft. PerceptionSimulation. ISimulatedEyes. WorldPosition**</span><span class="sxs-lookup"><span data-stu-id="df69d-507">**Microsoft.PerceptionSimulation.ISimulatedEyes.WorldPosition**</span></span>

<span data-ttu-id="df69d-508">Récupérer la position du nœud par rapport au monde, en mètres.</span><span class="sxs-lookup"><span data-stu-id="df69d-508">Retrieve the position of the node with relation to the world, in meters.</span></span>


### <a name="microsoftperceptionsimulationisimulationrecording"></a><span data-ttu-id="df69d-509">Microsoft. PerceptionSimulation. ISimulationRecording</span><span class="sxs-lookup"><span data-stu-id="df69d-509">Microsoft.PerceptionSimulation.ISimulationRecording</span></span>

<span data-ttu-id="df69d-510">Interface pour l’interaction avec un enregistrement unique chargé pour la lecture.</span><span class="sxs-lookup"><span data-stu-id="df69d-510">Interface for interacting with a single recording loaded for playback.</span></span>

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

<span data-ttu-id="df69d-511">**Microsoft. PerceptionSimulation. ISimulationRecording. DataTypes**</span><span class="sxs-lookup"><span data-stu-id="df69d-511">**Microsoft.PerceptionSimulation.ISimulationRecording.DataTypes**</span></span>

<span data-ttu-id="df69d-512">Récupère la liste des types de données dans l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="df69d-512">Retrieves the list of data types in the recording.</span></span>

<span data-ttu-id="df69d-513">**Microsoft. PerceptionSimulation. ISimulationRecording. State**</span><span class="sxs-lookup"><span data-stu-id="df69d-513">**Microsoft.PerceptionSimulation.ISimulationRecording.State**</span></span>

<span data-ttu-id="df69d-514">Récupère l’état actuel de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="df69d-514">Retrieves the current state of the recording.</span></span>

<span data-ttu-id="df69d-515">**Microsoft. PerceptionSimulation. ISimulationRecording. Play**</span><span class="sxs-lookup"><span data-stu-id="df69d-515">**Microsoft.PerceptionSimulation.ISimulationRecording.Play**</span></span>

<span data-ttu-id="df69d-516">Démarrez la lecture.</span><span class="sxs-lookup"><span data-stu-id="df69d-516">Start the playback.</span></span> <span data-ttu-id="df69d-517">Si l’enregistrement est suspendu, la lecture reprendra à partir de l’emplacement suspendu; s’il est arrêté, la lecture démarre au début.</span><span class="sxs-lookup"><span data-stu-id="df69d-517">If the recording is paused, playback will resume from the paused location; if stopped, playback will start at the beginning.</span></span> <span data-ttu-id="df69d-518">Si elle est déjà en cours d’exécution, cet appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="df69d-518">If already playing, this call is ignored.</span></span>

<span data-ttu-id="df69d-519">**Microsoft. PerceptionSimulation. ISimulationRecording. pause**</span><span class="sxs-lookup"><span data-stu-id="df69d-519">**Microsoft.PerceptionSimulation.ISimulationRecording.Pause**</span></span>

<span data-ttu-id="df69d-520">Suspend la lecture à son emplacement actuel.</span><span class="sxs-lookup"><span data-stu-id="df69d-520">Pauses the playback at its current location.</span></span> <span data-ttu-id="df69d-521">Si l’enregistrement est arrêté, l’appel est ignoré.</span><span class="sxs-lookup"><span data-stu-id="df69d-521">If the recording is stopped, the call is ignored.</span></span>

<span data-ttu-id="df69d-522">**Microsoft. PerceptionSimulation. ISimulationRecording. Seek (System. UInt64)**</span><span class="sxs-lookup"><span data-stu-id="df69d-522">**Microsoft.PerceptionSimulation.ISimulationRecording.Seek(System.UInt64)**</span></span>

<span data-ttu-id="df69d-523">Recherche l’enregistrement à l’heure spécifiée (dans les intervalles de 100 nanosecondes à partir du début) et s’interrompt à cet emplacement.</span><span class="sxs-lookup"><span data-stu-id="df69d-523">Seeks the recording to the specified time (in 100 nanoseconds intervals from the beginning) and pauses at that location.</span></span> <span data-ttu-id="df69d-524">Si l’heure est postérieure à la fin de l’enregistrement, elle est mise en pause au niveau de la dernière image.</span><span class="sxs-lookup"><span data-stu-id="df69d-524">If the time is beyond the end of the recording, it is paused at the last frame.</span></span>

<span data-ttu-id="df69d-525">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-525">Parameters</span></span>
* <span data-ttu-id="df69d-526">cycles: heure à laquelle effectuer la recherche.</span><span class="sxs-lookup"><span data-stu-id="df69d-526">ticks - The time to which to seek.</span></span>

<span data-ttu-id="df69d-527">**Microsoft. PerceptionSimulation. ISimulationRecording. Stop**</span><span class="sxs-lookup"><span data-stu-id="df69d-527">**Microsoft.PerceptionSimulation.ISimulationRecording.Stop**</span></span>

<span data-ttu-id="df69d-528">Arrête la lecture et réinitialise la position au début.</span><span class="sxs-lookup"><span data-stu-id="df69d-528">Stops the playback and resets the position to the beginning.</span></span>

### <a name="microsoftperceptionsimulationisimulationrecordingcallback"></a><span data-ttu-id="df69d-529">Microsoft. PerceptionSimulation. ISimulationRecordingCallback</span><span class="sxs-lookup"><span data-stu-id="df69d-529">Microsoft.PerceptionSimulation.ISimulationRecordingCallback</span></span>

<span data-ttu-id="df69d-530">Interface pour la réception des modifications d’État pendant la lecture.</span><span class="sxs-lookup"><span data-stu-id="df69d-530">Interface for receiving state changes during playback.</span></span>

```
public interface ISimulationRecordingCallback
{
    void PlaybackStateChanged(PlaybackState newState);
};
```

<span data-ttu-id="df69d-531">**Microsoft. PerceptionSimulation. ISimulationRecordingCallback. PlaybackStateChanged (Microsoft. PerceptionSimulation. PlaybackState)**</span><span class="sxs-lookup"><span data-stu-id="df69d-531">**Microsoft.PerceptionSimulation.ISimulationRecordingCallback.PlaybackStateChanged(Microsoft.PerceptionSimulation.PlaybackState)**</span></span>

<span data-ttu-id="df69d-532">Appelé lorsque l’état de lecture d’un ISimulationRecording a changé.</span><span class="sxs-lookup"><span data-stu-id="df69d-532">Called when an ISimulationRecording's playback state has changed.</span></span>

<span data-ttu-id="df69d-533">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-533">Parameters</span></span>
* <span data-ttu-id="df69d-534">newState: nouvel état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="df69d-534">newState - The new state of the recording.</span></span>

### <a name="microsoftperceptionsimulationperceptionsimulationmanager"></a><span data-ttu-id="df69d-535">Microsoft. PerceptionSimulation. PerceptionSimulationManager</span><span class="sxs-lookup"><span data-stu-id="df69d-535">Microsoft.PerceptionSimulation.PerceptionSimulationManager</span></span>

<span data-ttu-id="df69d-536">Objet racine pour la création d’objets de simulation de perception.</span><span class="sxs-lookup"><span data-stu-id="df69d-536">Root object for creating Perception Simulation objects.</span></span>

```
public static class PerceptionSimulationManager
{
    public static IPerceptionSimulationManager CreatePerceptionSimulationManager(ISimulationStreamSink sink);
    public static ISimulationStreamSink CreatePerceptionSimulationRecording(string path);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory);
    public static ISimulationRecording LoadPerceptionSimulationRecording(string path, ISimulationStreamSinkFactory factory, ISimulationRecordingCallback callback);
```

<span data-ttu-id="df69d-537">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationManager (Microsoft. PerceptionSimulation. ISimulationStreamSink)**</span><span class="sxs-lookup"><span data-stu-id="df69d-537">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationManager(Microsoft.PerceptionSimulation.ISimulationStreamSink)**</span></span>

<span data-ttu-id="df69d-538">Créez sur un objet pour générer des paquets simulés et les fournir au récepteur fourni.</span><span class="sxs-lookup"><span data-stu-id="df69d-538">Create on object for generating simulated packets and delivering them to the provided sink.</span></span>

<span data-ttu-id="df69d-539">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-539">Parameters</span></span>
* <span data-ttu-id="df69d-540">Sink: récepteur qui recevra tous les paquets générés.</span><span class="sxs-lookup"><span data-stu-id="df69d-540">sink - The sink that will receive all generated packets.</span></span>

<span data-ttu-id="df69d-541">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df69d-541">Return value</span></span>

<span data-ttu-id="df69d-542">Gestionnaire créé.</span><span class="sxs-lookup"><span data-stu-id="df69d-542">The created Manager.</span></span>

<span data-ttu-id="df69d-543">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. CreatePerceptionSimulationRecording (System. String)**</span><span class="sxs-lookup"><span data-stu-id="df69d-543">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.CreatePerceptionSimulationRecording(System.String)**</span></span>

<span data-ttu-id="df69d-544">Créez un récepteur qui stocke tous les paquets reçus dans un fichier au chemin d’accès spécifié.</span><span class="sxs-lookup"><span data-stu-id="df69d-544">Create a sink which stores all received packets in a file at the specified path.</span></span>

<span data-ttu-id="df69d-545">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-545">Parameters</span></span>
* <span data-ttu-id="df69d-546">chemin d’accès: chemin d’accès du fichier à créer.</span><span class="sxs-lookup"><span data-stu-id="df69d-546">path - The path of the file to create.</span></span>

<span data-ttu-id="df69d-547">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df69d-547">Return value</span></span>

<span data-ttu-id="df69d-548">Récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="df69d-548">The created sink.</span></span>

<span data-ttu-id="df69d-549">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory)**</span><span class="sxs-lookup"><span data-stu-id="df69d-549">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory)**</span></span>

<span data-ttu-id="df69d-550">Charge un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="df69d-550">Load a recording from the specified file.</span></span>

<span data-ttu-id="df69d-551">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-551">Parameters</span></span>
* <span data-ttu-id="df69d-552">chemin d’accès: chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="df69d-552">path - The path of the file to load.</span></span>
* <span data-ttu-id="df69d-553">Factory: fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="df69d-553">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>

<span data-ttu-id="df69d-554">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df69d-554">Return value</span></span>

<span data-ttu-id="df69d-555">Enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="df69d-555">The loaded recording.</span></span>

<span data-ttu-id="df69d-556">**Microsoft. PerceptionSimulation. PerceptionSimulationManager. LoadPerceptionSimulationRecording (System. String, Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory, Microsoft. PerceptionSimulation. ISimulationRecordingCallback)**</span><span class="sxs-lookup"><span data-stu-id="df69d-556">**Microsoft.PerceptionSimulation.PerceptionSimulationManager.LoadPerceptionSimulationRecording(System.String,Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory,Microsoft.PerceptionSimulation.ISimulationRecordingCallback)**</span></span>

<span data-ttu-id="df69d-557">Charge un enregistrement à partir du fichier spécifié.</span><span class="sxs-lookup"><span data-stu-id="df69d-557">Load a recording from the specified file.</span></span>

<span data-ttu-id="df69d-558">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-558">Parameters</span></span>
* <span data-ttu-id="df69d-559">chemin d’accès: chemin d’accès du fichier à charger.</span><span class="sxs-lookup"><span data-stu-id="df69d-559">path - The path of the file to load.</span></span>
* <span data-ttu-id="df69d-560">Factory: fabrique utilisée par l’enregistrement pour créer un ISimulationStreamSink quand cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="df69d-560">factory - A factory used by the recording for creating an ISimulationStreamSink when required.</span></span>
* <span data-ttu-id="df69d-561">callback: rappel qui reçoit les mises à jour qui regradent l’état de l’enregistrement.</span><span class="sxs-lookup"><span data-stu-id="df69d-561">callback - A callback which receives updates regrading the recording's status.</span></span>

<span data-ttu-id="df69d-562">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df69d-562">Return value</span></span>

<span data-ttu-id="df69d-563">Enregistrement chargé.</span><span class="sxs-lookup"><span data-stu-id="df69d-563">The loaded recording.</span></span>

### <a name="microsoftperceptionsimulationstreamdatatypes"></a><span data-ttu-id="df69d-564">Microsoft. PerceptionSimulation. StreamDataTypes</span><span class="sxs-lookup"><span data-stu-id="df69d-564">Microsoft.PerceptionSimulation.StreamDataTypes</span></span>

<span data-ttu-id="df69d-565">Décrit les différents types de données de flux.</span><span class="sxs-lookup"><span data-stu-id="df69d-565">Describes the different types of stream data.</span></span>

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

<span data-ttu-id="df69d-566">**Microsoft. PerceptionSimulation. StreamDataTypes. None**</span><span class="sxs-lookup"><span data-stu-id="df69d-566">**Microsoft.PerceptionSimulation.StreamDataTypes.None**</span></span>

<span data-ttu-id="df69d-567">Valeur de sentinelle utilisée pour indiquer l’absence de type de données de flux.</span><span class="sxs-lookup"><span data-stu-id="df69d-567">A sentinel value used to indicate no stream data types.</span></span>

<span data-ttu-id="df69d-568">**Microsoft. PerceptionSimulation. StreamDataTypes. Head**</span><span class="sxs-lookup"><span data-stu-id="df69d-568">**Microsoft.PerceptionSimulation.StreamDataTypes.Head**</span></span>

<span data-ttu-id="df69d-569">Flux de données concernant la position et l’orientation de l’en-tête.</span><span class="sxs-lookup"><span data-stu-id="df69d-569">Stream of data regarding the position and orientation of the head.</span></span>

<span data-ttu-id="df69d-570">**Microsoft. PerceptionSimulation. StreamDataTypes. mains**</span><span class="sxs-lookup"><span data-stu-id="df69d-570">**Microsoft.PerceptionSimulation.StreamDataTypes.Hands**</span></span>

<span data-ttu-id="df69d-571">Flux de données concernant la position et les gestes des mains.</span><span class="sxs-lookup"><span data-stu-id="df69d-571">Stream of data regarding the position and gestures of hands.</span></span>

<span data-ttu-id="df69d-572">**Microsoft. PerceptionSimulation. StreamDataTypes. SpatialMapping**</span><span class="sxs-lookup"><span data-stu-id="df69d-572">**Microsoft.PerceptionSimulation.StreamDataTypes.SpatialMapping**</span></span>

<span data-ttu-id="df69d-573">Flux de données concernant le mappage spatial de l’environnement.</span><span class="sxs-lookup"><span data-stu-id="df69d-573">Stream of data regarding spatial mapping of the environment.</span></span>

<span data-ttu-id="df69d-574">**Microsoft. PerceptionSimulation. StreamDataTypes. étalonnage**</span><span class="sxs-lookup"><span data-stu-id="df69d-574">**Microsoft.PerceptionSimulation.StreamDataTypes.Calibration**</span></span>

<span data-ttu-id="df69d-575">Flux de données concernant l’étalonnage de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="df69d-575">Stream of data regarding calibration of the device.</span></span> <span data-ttu-id="df69d-576">Les paquets d’étalonnage sont acceptés uniquement par un système en mode distant.</span><span class="sxs-lookup"><span data-stu-id="df69d-576">Calibration packets are only accepted by a system in Remote Mode.</span></span>

<span data-ttu-id="df69d-577">**Microsoft. PerceptionSimulation. StreamDataTypes. Environment**</span><span class="sxs-lookup"><span data-stu-id="df69d-577">**Microsoft.PerceptionSimulation.StreamDataTypes.Environment**</span></span>

<span data-ttu-id="df69d-578">Flux de données concernant l’environnement de l’appareil.</span><span class="sxs-lookup"><span data-stu-id="df69d-578">Stream of data regarding the environment of the device.</span></span>

<span data-ttu-id="df69d-579">**Microsoft. PerceptionSimulation. StreamDataTypes. All**</span><span class="sxs-lookup"><span data-stu-id="df69d-579">**Microsoft.PerceptionSimulation.StreamDataTypes.All**</span></span>

<span data-ttu-id="df69d-580">Valeur de sentinelle utilisée pour indiquer tous les types de données enregistrés.</span><span class="sxs-lookup"><span data-stu-id="df69d-580">A sentinel value used to indicate all recorded data types.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsink"></a><span data-ttu-id="df69d-581">Microsoft. PerceptionSimulation. ISimulationStreamSink</span><span class="sxs-lookup"><span data-stu-id="df69d-581">Microsoft.PerceptionSimulation.ISimulationStreamSink</span></span>

<span data-ttu-id="df69d-582">Objet qui reçoit les paquets de données d’un flux de simulation.</span><span class="sxs-lookup"><span data-stu-id="df69d-582">An object that receives data packets from a simulation stream.</span></span>

```
public interface ISimulationStreamSink
{
    void OnPacketReceived(uint length, byte[] packet);
}
```

<span data-ttu-id="df69d-583">**Microsoft. PerceptionSimulation. ISimulationStreamSink. OnPacketReceived (uint Length, Byte [] paquet)**</span><span class="sxs-lookup"><span data-stu-id="df69d-583">**Microsoft.PerceptionSimulation.ISimulationStreamSink.OnPacketReceived(uint length, byte[] packet)**</span></span>

<span data-ttu-id="df69d-584">Reçoit un paquet unique, qui est typé en interne et avec version.</span><span class="sxs-lookup"><span data-stu-id="df69d-584">Receives a single packet, which is internally typed and versioned.</span></span>

<span data-ttu-id="df69d-585">Paramètres</span><span class="sxs-lookup"><span data-stu-id="df69d-585">Parameters</span></span>
* <span data-ttu-id="df69d-586">Length-Longueur du paquet.</span><span class="sxs-lookup"><span data-stu-id="df69d-586">length - The length of the packet.</span></span>
* <span data-ttu-id="df69d-587">paquet: données du paquet.</span><span class="sxs-lookup"><span data-stu-id="df69d-587">packet - The data of the packet.</span></span>

### <a name="microsoftperceptionsimulationisimulationstreamsinkfactory"></a><span data-ttu-id="df69d-588">Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory</span><span class="sxs-lookup"><span data-stu-id="df69d-588">Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory</span></span>

<span data-ttu-id="df69d-589">Objet qui crée ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="df69d-589">An object that creates ISimulationStreamSink.</span></span>

```
public interface ISimulationStreamSinkFactory
{
    ISimulationStreamSink CreateSimulationStreamSink();
}
```

<span data-ttu-id="df69d-590">**Microsoft. PerceptionSimulation. ISimulationStreamSinkFactory. CreateSimulationStreamSink ()**</span><span class="sxs-lookup"><span data-stu-id="df69d-590">**Microsoft.PerceptionSimulation.ISimulationStreamSinkFactory.CreateSimulationStreamSink()**</span></span>

<span data-ttu-id="df69d-591">Crée une seule instance de ISimulationStreamSink.</span><span class="sxs-lookup"><span data-stu-id="df69d-591">Creates a single instance of ISimulationStreamSink.</span></span>

<span data-ttu-id="df69d-592">Valeur de retour</span><span class="sxs-lookup"><span data-stu-id="df69d-592">Return value</span></span>

<span data-ttu-id="df69d-593">Récepteur créé.</span><span class="sxs-lookup"><span data-stu-id="df69d-593">The created sink.</span></span>
